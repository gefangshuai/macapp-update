<template>
    <div id="app">
        <div class="container">
            <div class="row ">
                <div class="col-md-12 mar-top">
                    <div class="page-header">
                        <h4 class="title">软件更新列表</h4>
                    </div>
                    <router-view></router-view>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'macapp-update',
        methods: {
            navHome(){
                this.$router.push('/');
            }
        }
    }
</script>

<style>
    /* CSS */
    @import "./assets/main.scss";
    #app {
        padding: 20px 0;
    }
    .title {
        font-weight: normal;;
    }

</style>
