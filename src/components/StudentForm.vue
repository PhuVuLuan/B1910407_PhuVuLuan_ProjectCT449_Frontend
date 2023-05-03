<template>
    <Form
        @submit="submitStudent"
        :validation-schema="studentFormSchema"
    >
        <div class="form-group">
            <label for="name">Tên</label>
            <Field
                name="name"
                type="text"
                class="form-control"
                v-model="studentLocal.name"
            />
            <ErrorMessage name="name" class="error-feedback" />
        </div>

        <div class="form-group">
            <label for="mssv">Mã số</label>
            <Field
                name="mssv"
                type="text"
                class="form-control"
                v-model="studentLocal.mssv"
            />
            <ErrorMessage name="mssv" class="error-feedback" />
        </div>

        <div class="form-group">
            <label for="makhoa">Mã khoa</label>
            <Field
                name="makhoa"
                type="text"
                class="form-control"
                v-model="studentLocal.maKhoa"
            />
            <ErrorMessage name="makhoa" class="error-feedback" />
        </div>

        <div class="form-group">
            <label for="tenkhoa">Tên khoa</label>
            <Field
                name="tenkhoa"
                type="text"
                class="form-control"
                v-model="studentLocal.tenKhoa"
            />
            <ErrorMessage name="tenkhoa" class="error-feedback" />
        </div>

        <div class="form-group">
            <label for="bithday">Ngày sinh</label>
            <Field
                name="bithday"
                type="date"
                class="form-control"
                v-model="studentLocal.bithday"
            />
            <ErrorMessage name="bithday" class="error-feedback" />
        </div>

        <div class="form-group">
            <label for="bithplace">Nơi sinh</label>
            <Field
                name="bithplace"
                type="text"
                class="form-control"
                v-model="studentLocal.bithplace"
            />
            <ErrorMessage name="bithplace" class="error-feedback" />
        </div>

        <div class="form-group">
            <label for="email">E-mail</label>
            <Field
                name="email"
                type="email"
                class="form-control"
                v-model="studentLocal.email"
            />
            <ErrorMessage name="email" class="error-feedback" />
        </div>
        <div class="form-group">
            <label for="address">Địa chỉ</label>
            <Field
                name="address"
                type="text"
                class="form-control"
                v-model="studentLocal.address"
            />
            <ErrorMessage name="address" class="error-feedback" />
        </div>
        <div class="form-group">
            <label for="phone">Điện thoại</label>
            <Field
                name="phone"
                type="tel"
                class="form-control"
                v-model="studentLocal.phone"
            />
            <ErrorMessage name="phone" class="error-feedback" />
        </div>
        
        <div class="form-group">
            <button class="btn btn-primary">Lưu</button>
            <button
                v-if="studentLocal._id"
                type="button"
                class="ml-2 btn btn-danger"
                @click="deleteStudent"
            >
                Xóa
            </button>
        </div>
    </Form>
</template>

<script>
    import * as yup from "yup";
    import { Form, Field, ErrorMessage } from "vee-validate";
    export default {
        components: {
            Form,
            Field,
            ErrorMessage,
        },
        emits: ["submit:student", "delete:student"],
        props: {
            student: { type: Object, required: true }
        },
        data() {
            const studentFormSchema = yup.object().shape({
                name: yup
                .string()
                .required("Tên phải có giá trị.")
                .min(2, "Tên phải ít nhất 2 ký tự.")
                .max(50, "Tên có nhiều nhất 50 ký tự."),
                email: yup
                .string()
                .email("E-mail không đúng.")
                .max(50, "E-mail tối đa 50 ký tự."),
                address: yup.string().max(100, "Địa chỉ tối đa 100 ký tự."),
                phone: yup
                .string()
                .matches(
                /((09|03|07|08|05)+([0-9]{8})\b)/g,
                "Số điện thoại không hợp lệ."
                ),
            });
            return {
                studentLocal: this.student,
                studentFormSchema,
            };
        },
        methods: {
            submitStudent() {
                this.$emit("submit:student", this.studentLocal);
            },
            deleteStudent() {
                this.$emit("delete:student", this.studentLocal.id);
            },
        },
    };
</script>

<style scoped>
    @import "@/assets/form.css";
</style>
    