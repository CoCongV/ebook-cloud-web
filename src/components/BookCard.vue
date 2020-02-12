<template>
    <a-card hoverable style="width: 80%;">
        <img alt="book cover img" :src="book.CoverImg" slot="cover"/>
        <template class="ant-card-actions" slot="actions">
            <a-icon type="cloud-download" @click="download"/>
            <a-icon type="ellipsis"/>
        </template>
        <a-card-meta :title="book.Name">
            <template slot="description">
                Authors:
                <span v-for="author in book.Authors" :key="author.ID">{{author.Name}}</span>
            </template>
        </a-card-meta>
    </a-card>
</template>

<script>
import { api } from "@/util/api";
export default {
    props: ["book"],
    data() {
        return {};
    },
    methods: {
        download() {
            const fileDownload = require('js-file-download');
            let url = api.book.replace(":id", this.book.id)
            let ss = this.book.File.split("/")
            let filename = ss[ss.length-1]
            this.axios.get(url).then((response) => {
                fileDownload(response.data, filename)
            }).catch((error) => {
                console.log(error)
            })

        }
    }
};
</script>
