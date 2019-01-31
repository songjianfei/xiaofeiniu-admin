<template>
  <div class="categorylist">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">首页</el-breadcrumb-item>
      <el-breadcrumb-item>菜品类别管理</el-breadcrumb-item>
      <el-breadcrumb-item>类别列表</el-breadcrumb-item>
    </el-breadcrumb>
    <el-button type="primary" size="mini" @click="addCategory">+  添加新的菜品类别</el-button>
    <el-table :data="categoryList" size="small" stripe border>
      <el-table-column label='编号' prop='cid'></el-table-column>
      <el-table-column label='名称' prop='cname'></el-table-column>
      <el-table-column label='操作'>
        <template slot-scope="{row,$index}">
          <el-button type="success" @click="updateCategory($index,row)" size="mini">修改</el-button>
          <el-button type="danger" @click="deleteCategory($index,row)" size="mini">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      categoryList:[]
    }
  },
  methods: {
    updateCategory(cid,row){
      this.$prompt('请输入新的菜品类别名称：','修改菜品名称分类',{
        inputValue:row.cname
      }).then(val=>{
        var data={cid:row.cid,cname:val.value}
        var url=this.$store.state.globalSettings.apiUrl+'/admin/category'
        this.$axios.put(url,data).then(res=>{
          if(res.data.code==200){
            this.$message.success('類別修改成功！')
            this.categoryList.splice(cid,1,{cid:data.cid,cname:data.cname})
          }
        })
      })
    },
    deleteCategory(cid,row){
      this.$confirm('删除操作不可撤销，您确定吗？','提示',{type:'warning'}).then(()=>{
          var url=this.$store.state.globalSettings.apiUrl+'/admin/category/'+row.cid;
        this.$axios.delete(url).then(res=>{
          if(res.data.code==200){
            this.categoryList.splice(cid,1);
            this.$message.success('菜品类别删除成功！')
          }else{
            this.$message.error('类别删除出错了'+res.data.msg)
          }
      }).catch(err=>{
        console.log(err)
      })
      }).catch(err=>{
        console.log(err);
      })
      
    },
    addCategory(){
      this.$prompt('請輸入新的類別名：','提示',{type:'info'}).then(({value})=>{
        console.log(value);
        var url=this.$store.state.globalSettings.apiUrl+'/admin/category';
        this.$axios.post(url,{cname:value}).then(res=>{
          if(res.data.code==200){
            this.$message.success('新的類別添加成功！')
            //模型數據中添加新的類別
            this.categoryList.push({cid:res.data.cid,cname:value})
          }else{
            this.$message.error('新的類別添加出錯：'+res.data.msg)
          }
        }).catch(err=>{
          console.log(err);
        })
      }).catch(err=>{console.log(err)})
    }
  },
  created() {
    var url=this.$store.state.globalSettings.apiUrl+'/admin/category';
    this.$axios.get(url).then(res=>{
      this.categoryList=res.data;
    }).catch(err=>{
      console.log(err)
    })
  },
}
</script>
<style lang="scss">
.categorylist .el-breadcrumb{
  margin-bottom: 20px;
}
.categorylist .el-button{
  margin-bottom: 5px;
}
</style>

