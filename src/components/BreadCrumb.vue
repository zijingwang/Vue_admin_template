<template>
    <el-breadcrumb separator-class="el-icon-arrow-right">
        <transition-group name="breadcrumb">
            <el-breadcrumb-item v-for="(item,index) in levelList" :key="item.path" v-if="item.meta.title">
                <span v-if="index === levelList.length-1" class="no-redirect">{{item.meta.title}}</span>
                <router-link v-else :to="item.redirect || item.path">{{item.meta.title}}</router-link>
            </el-breadcrumb-item>
        </transition-group>
    </el-breadcrumb>
</template>

<script>
export default {
    name: 'BreadCrumb',
    data() {
        return {
            levelList: null
        }
    },
    watch: {
        $route() {
            this.getBreadcrumb()
        }
    },
    created() {
        this.getBreadcrumb()
    },
    methods: {
        getBreadcrumb() {

            let matched = this.$route.matched.filter(item => item.name)
//            console.log(matched)
            const first = matched[0]

            if (first && first.name !== 'home') {
                matched = [{ path: '/home', meta: { title: '首页' }}].concat(matched)
            }
            this.levelList = matched
        }
    }
}
</script>
