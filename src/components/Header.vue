<template>
    <div>
        <a-icon
          :class="this.checked ? 'trigger-dark' : 'trigger'"
          :type="collapsed ? 'menu-unfold' : 'menu-fold'"
          @click="Triger"
        />
        <a-switch
            defaultChecked
            :checked="checked"
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
            checked: false
        }
    },
    methods: {
        Triger() {
            this.collapsed = !this.collapsed
            this.$emit("Triger", this.collapsed)
            localStorage.setItem("collapsed", this.collapsed)
        },
        changeTheme(checked) {
            let theme = checked ? "dark" : "light"
            this.checked = checked
            this.$emit("changeTheme", theme)
            localStorage.setItem("theme", theme)
        }
    },
    mounted() {
        console.log(localStorage.getItem("theme"))
        this.checked = localStorage.getItem("theme") == 'dark' ? true : false
        this.collapsed = localStorage.getItem("collapsed") =='true' ? true : false
    }
}
</script>

<style scoped>
.trigger {
    font-size: 18px;
    line-height: 66px;
    padding: 0 24px;
    cursor: pointer;
    transition: color 0.3s;
  }
.trigger:hover {
    color: #1890ff;
}
.trigger-dark {
    font-size: 18px;
    line-height: 66px;
    padding: 0 24px;
    cursor: pointer;
    transition: color 0.3s;
    color: #fff;
}
</style>