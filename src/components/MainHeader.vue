<template>
    <div class='my-main-header'>
        <h3 class='my-title'>{{$store.state.globalSettings.appName}}管理后台</h3>
        <div class='my-right'>
            当前用户：{{$store.state.adminName}}
            <el-button size="mini" @click="quit">退出</el-button>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            
        }
    },
    methods: {
        quit(){
            //清除当前用户登录信息
            this.$store.commit('setAdminName','');
            //跳转回登录页
            this.$router.push('/login')
        }
    },
}
</script>
<style lang="scss">
.my-main-header{
    background: #EBEEF5;
    border-radius: 4px;
    line-height: 60px;
    padding: 0 8px;
    .my-title{
        color:#303133;
        display: inline;
    }
    .my-right{
        float: right;
        button{
            margin-left:8px;
        }
    }
}
</style>
