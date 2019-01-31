<template>
  <div class="security">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">首页</el-breadcrumb-item>
      <el-breadcrumb-item>安全管理</el-breadcrumb-item>
    </el-breadcrumb>
    <el-card shadow="never" class="my-card">
      <div slot="header">
        <span>修改管理员密码</span>
      </div>
      <el-form label-width="110px">
        <el-form-item label="旧密码：">
          <el-input placeholder="请输入旧密码">
          </el-input>
        </el-form-item>
        <el-form-item label="新密码：">
          <el-input placeholder="请输入新密码">
          </el-input>
        </el-form-item>
        <el-form-item label="再输入一次：">
          <el-input placeholder="请确认密码">
          </el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary">确认</el-button>
          <el-button>取消</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>
<script>
export default {
  
}
</script>
<style lang="scss">
.security .el-breadcrumb{
  margin-bottom: 20px;
}
.security .my-card{
  width:550px;
}
</style>

