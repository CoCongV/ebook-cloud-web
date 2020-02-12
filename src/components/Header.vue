<template>
    <div>
        <a-icon
          class="trigger"
          :type="collapsed ? 'menu-unfold' : 'menu-fold'"
          @click="Triger"
        />
        <a-switch
            defaultChecked
            @change="changeTheme"
            checkedChildren="dark"
            unCheckedChildren="light"
        />
    </div>
</template>

<script>
export default {
    data() {
        return {
            collapsed: false,
            light: true
        }
    },
    methods: {
        Triger() {
            this.collapsed = !this.collapsed
            this.$emit("Triger", this.collapsed)
        },
        changeTheme(checked) {
            this.light = checked ? false : true
            let theme = checked ? "dark" : "light"
            this.$emit("changeTheme", theme)
        }
    }
}
</script>

<style scoped>
.trigger {
    font-size: 18px;
    line-height: 64px;
    padding: 0 24px;
    cursor: pointer;
    transition: color 0.3s;
  }
.trigger:hover {
    color: #1890ff;
}
</style>