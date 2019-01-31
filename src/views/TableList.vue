<template>
  <div class="tablelist">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">首页</el-breadcrumb-item>
      <el-breadcrumb-item>桌台管理</el-breadcrumb-item>  
      <el-breadcrumb-item>桌台列表</el-breadcrumb-item>    
    </el-breadcrumb>
    <el-row>
      <el-col v-for="(t,i) in tablelist" :key="i" :xs="12" :sm="8" :md="6" :lg="4" :xl="2">
        <my-table :data='t'></my-table>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import Table from '../components/Table'
export default {
  data() {
    return {
      tablelist:[]
    }
  },
  created() {
    var url=this.$store.state.globalSettings.apiUrl+'/admin/table'
    this.$axios.get(url).then(res=>{
      this.tablelist=res.data
    })
  },
  components:{
    'my-table':Table
  }
}
</script>
<style lang="scss">
.tablelist .el-breadcrumb{
  margin-bottom:20px; 
} 
</style>

