<template>
    <nav class="navbar navbar-expand navbar-dark bg-dark" style="position: absolute; top: -5vw; width: 96vw;">
        <a href="/" class="navbar-brand">Ứng dụng Quản lý sinh viên</a>
        <div class="mr-auto navbar-nav">
            <li class="nav-item">
                <router-link :to="{ name: 'studentmanager' }" class="nav-link">
                    Danh sách sinh viên
                    <i class="fas fa-address-book"></i>
                </router-link>
            </li>
        </div>
    </nav>
</template>