<template>
    <div class="page row" style="width: 1200px">
        <div class="col-md-10">
            <InputSearch v-model="searchText" />
        </div>
        <div class="mt-3 col-md-6">
            <h4>
                Sinh viên
                <i class="fas fa-address-book"></i>
            </h4>
            <StudentList
                v-if="filteredStudentsCount > 0"
                :students="filteredStudents"
                v-model:activeIndex="activeIndex"
            />
            <p v-else>Không có liên hệ nào.</p>
            <div class="mt-3 row justify-content-around align-items-center">
                <button class="btn btn-sm btn-primary" @click="refreshList()">
                    <i></i> Làm mới
                </button>
                <button class="btn btn-sm btn-success" @click="goToAddStudent">
                    <i class="fas fa-plus"></i> Thêm mới
                </button>
                <button
                    class="btn btn-sm btn-danger"
                    @click="removeAllStudents"
                >
                    <i class="fas fa-trash-alt"></i> Xóa tất cả
                </button>
            </div>
        </div>
        <div class="mt-3 col-md-6">
            <div v-if="activeStudent">
                <h4>
                    Chi tiết Liên hệ
                    <i class="fas fa-address-card"></i>
                </h4>
                <StudentCard :student="activeStudent" />
                <router-link
                        :to="{
                        name: 'student.edit',
                        params: { id: activeStudent._id },
                        }"
                    >
                    <span class="mt-2 badge badge-warning">
                        <i class="fas fa-edit"></i> Hiệu chỉnh
                    </span>
                </router-link>
            </div>
        </div>
    </div>
</template>

<script>
    import StudentCard from "@/components/StudentCard.vue";
    import InputSearch from "@/components/InputSearch.vue";
    import StudentList from "@/components/StudentList.vue";
    import StudentService from "@/services/student.service";
    export default {
    components: {
        StudentCard,
        InputSearch,
        StudentList,
    },
    data() {
        return {
        students: [],
        activeIndex: -1,
        searchText: "",
        };
    },
    watch: {
    // Giám sát các thay đổi của biến searchText.
    // Bỏ chọn phần tử đang được chọn trong danh sách.
        searchText() {
        this.activeIndex = -1;
        },
    },
    computed: {
    // Chuyển các đối tượng student thành chuỗi để tiện cho tìm kiếm.
        studentStrings() {
            return this.students.map((student) => {
                const { name, email, address, phone } = student;
                return [name, email, address, phone].join("");
            });
        },
        // Trả về các student có chứa thông tin cần tìm kiếm.
        filteredStudents() {
            if (!this.searchText) return this.students;
            return this.students.filter((_student, index) =>
                this.studentStrings[index].includes(this.searchText)
            );
        },
        activeStudent() {
            if (this.activeIndex < 0) return null;
            return this.filteredStudents[this.activeIndex];
        },
        filteredStudentsCount() {
            return this.filteredStudents.length;
        },
    },
    methods: {
        async retrieveStudents() {
            try {
                this.students = await StudentService.getAll();
            } catch (error) {
                console.log(error);
            }
        },
        refreshList() {
            this.retrieveStudents();
            this.activeIndex = -1;
        },
        async removeAllStudents() {
            if (confirm("Bạn muốn xóa tất cả Liên hệ?")) {
            try {
                await StudentService.deleteAll();
                this.refreshList();
            } catch (error) {
                console.log(error);
            }
            }
        },
        goToAddStudent() {
            this.$router.push({ name: "student.add" });
        },
    },
    mounted() {
        this.refreshList();
    },
    };
    
</script>
<style scoped>
    .page {
        text-align: left;
        max-width: 750px;
    }
</style>