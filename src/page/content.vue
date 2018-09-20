<template>
    <div class="content">
        <myHeader></myHeader>

        <h2 v-if="dat.title"></h2>
        <p v-if="dat.author">作者：{{dat.author.loginname}}发表于：{{$utils.goodTime(dat.create_at)}}</p>
        <hr>
        <div class="article" v-html="dat.content"></div>
        <h3>网友回复：</h3>
        <ul>
            <li v-for="item in dat.replies" :key="item.id">
                <p>评论者：{{item.author.loginname}}评论与：{{$utils.goodTime(item.create_at)}}</p>
                <div class="article" v-html="item.content"></div>
            </li>
        </ul>
        <myFooter></myFooter>
    </div>
</template>

<script>
import myHeader from '../components/Header.vue'
import myFooter from '../components/Footer.vue'
export default {
    components:{myHeader, myFooter},
    data() {
        return {
            id: this.$route.params.id,
            dat:{}
        };
    },
    created() {
        this.getData();
    },
    methods: {
        getData() {
            this.$api.get("topic/" + this.id, null, r => {
                this.dat = r.data;
            });
        }
    }
};
</script>

<style>

</style>
