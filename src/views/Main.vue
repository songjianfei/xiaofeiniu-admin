<template>
  <div class="main">
    <el-container>
      <!--左侧的菜单栏-->
      <el-aside width="180px">
      </el-aside>
      <el-container>
        <!--顶部信息栏-->
        <el-header height="60px">顶部</el-header>
        <!--主体部分-->
        <el-main>主体
            <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>
<script>
export default {
  beforeCreate() {
    //组件创建之前先要检查是否已经登录
    if(!this.$store.state.adminName){
      this.$router.push('/login')
    }
  },
}
</script>
<style lang="scss">
 .main{
   margin:30px 0 0 30px;
 } 
</style>