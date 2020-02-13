<template>
    <a-pagination v-model="current" :total="count" pageSize="20" @change="onChange"/>
</template>

<script>
export default {
    props: ['count', 'current'],
    data() {
        return {
        };
    },
    methods: {
        onChange(pageNum) {
            this.$emit("onChange", pageNum)
        }
    }
};
</script>
