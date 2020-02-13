<template>
    <a-layout class="home">
        <a-layout-sider
            collapsible
            v-model="collapsed"
            :trigger="null"
            class="sider"
            :theme="theme"
        >
            <SlideBar :theme="theme"></SlideBar>
        </a-layout-sider>
        <a-layout
            :class="collapsed ? 'main-content-slider-off' : 'main-content-slider-on'"
            key="layout"
        >
            <a-layout-header
                key="layout-header"
                :class="this.theme == 'light' ? 'header-light' : 'header-dark'"
            >
                <Header @Triger="Trigger" @changeTheme="changeTheme" key="header"></Header>
            </a-layout-header>
            <a-layout-content key="content" class="content">
                <a-row>
                    <a-col :span="6" v-for="book in books" :key="book.ID" class="book-col">
                        <BookCard :book="book"></BookCard>
                    </a-col>
                </a-row>
            </a-layout-content>
            <a-layout-footer>
                <Pagination :count="count" :current="page" @onChange="changePage"></Pagination>
            </a-layout-footer>
        </a-layout>
    </a-layout>
</template>

<script>
import SlideBar from "@/components/SlideBar.vue";
import Header from "@/components/Header.vue";
import BookCard from "@/components/BookCard.vue";
import Pagination from "@/components/Pagination.vue";
import { api } from "@/util/api";

export default {
    components: {
        SlideBar,
        Header,
        BookCard,
        Pagination
    },
    data() {
        return {
            collapsed: false,
            theme: "light",
            books: [],
            prev: false,
            next: false,
            count: 0,
            page: 1
        };
    },
    methods: {
        Trigger(collapsed) {
            this.collapsed = collapsed;
        },
        changeTheme(theme) {
            this.theme = theme;
        },
        changePage(page) {
            this.page = page;
            this.getBooks()
        },
        getBooks() {
            this.axios
                .get(api.books, {
                    params: {
                        page: this.page
                    }
                })
                .then(response => {
                    this.books = response.data.books;
                    this.prev = response.data.prev;
                    this.next = response.data.next;
                    this.count = response.data.count;
                });
        }
    },
    mounted() {
        this.theme = localStorage.getItem("theme");
        this.collapsed =
            localStorage.getItem("collapsed") == "true" ? true : false;
        this.getBooks();
    }
};
</script>

<style>
.sider {
    overflow: auto;
    height: 100vh;
    position: fixed !important;
    left: 0;
}
.main-content-slider-on {
    margin-left: 200px;
    transition: all 0.2s;
}
.main-content-slider-off {
    margin-left: 80px;
    transition: all 0.2s;
}
.content {
    margin: 24px 16px;
    padding: 24px;
    min-height: 280px;
    background: #fff;
}
.header-light {
    background: #fff !important;
    padding: 0px !important;
    height: 66px !important;
}
.header-dark {
    background: #001529 !important;
    padding: 0px !important;
    height: 66px !important;
}
.book-col {
    margin-bottom: 8px;
}
</style>