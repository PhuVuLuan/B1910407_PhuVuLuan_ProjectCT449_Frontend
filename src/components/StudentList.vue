<script>
    export default {
        props: {
            students: { type: Array, default: [] },
            activeIndex: { type: Number, default: -1 },
        },
        emits: ["update:activeIndex"],
        methods: {
            updateActiveIndex(index) {
                this.$emit("update:activeIndex", index);
            }
        }
    };
</script>
<template>
    <ul class="list-group" style="color: black;">
        <li
            class="list-group-item"
            v-for="(student, index) in students"
            :key="student._id"
            :class="{ active: index === activeIndex }"
            @click="updateActiveIndex(index)"
        >
            {{ student.name }}
        </li>
    </ul>
</template>