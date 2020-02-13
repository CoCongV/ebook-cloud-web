<template>
    <div>
        <div class="logo" />
        <a-menu :theme="theme" mode="inline" :defaultSelectedKeys="['1']" class="sider-menu">
            <a-menu-item key="1">
                <a-icon type="home" />
                <span>主页</span>
            </a-menu-item>
            <a-sub-menu key="2">
                <span slot="title">
                    <a-icon type="hdd" />
                    <span>分类</span>
                </span>
                <a-menu-item key="2-1">国家</a-menu-item>
                <a-menu-item key="2-2">作者</a-menu-item>
                <a-menu-item key="2-3">标签</a-menu-item>
            </a-sub-menu>
            <a-sub-menu key="3">
                <span slot="title">
                    <a-icon type="user" />
                    <span>个人中心</span>
                </span>
                <a-menu-item key="3-1">个人资料</a-menu-item>
                <a-menu-item key="3-2">上传图书</a-menu-item>
            </a-sub-menu>
        </a-menu>
    </div>
</template>

<script>
export default {
    props: ["theme"],
    data() {
        return {
        }
    }
}
</script>

<style scoped>
.logo {
    height: 32px;
    background: rgba(255, 255, 255, 0.2);
    margin: 16px;
}
.sider-menu {
    border-right: 0px !important;
}
</style>