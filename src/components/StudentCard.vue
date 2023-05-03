<script>
    export default {
        props: {
            student: { type: Object, required: true },
        },
    };
</script>
<template>
    <div>
        <div class="p-1">
            <strong>Tên:</strong>
            {{ student.name }}
        </div>
        <div class="p-1">
            <strong>Giới tính:</strong>
            {{ student.gender }}
        </div>
        <div class="p-1">
            <strong>Ngày sinh:</strong>
            {{ student.bithday }}
        </div>
        <div class="p-1">
            <strong>Nơi sinh:</strong>
            {{ student.bithplace }}
        </div>
        <div class="p-1">
            <strong>E-mail:</strong>
            {{ student.email }}
        </div>
        <div class="p-1">
            <strong>Thuộc khoa:</strong>
            {{ student.maKhoa }} - {{ student.tenKhoa }}
        </div>
        <div class="p-1">
            <strong>Địa chỉ:</strong>
            {{ student.address }}
        </div>
        <div class="p-1">
            <strong>Điện thoại:</strong>
            {{ student.phone }}
        </div>
    </div>
</template>