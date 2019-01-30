<template>
  <div class="login">
    <el-card class="my-login-card">
      <div slot='header'>管理员登录</div>
      <div>
        <el-form label-width="100px">
          <el-form-item label="管理员名：">
            <el-input placeholder='请输入管理员名' v-model="formData.aname"></el-input>
          </el-form-item>
          <el-form-item label="登录密码：">
            <el-input placeholder='请输入管理员密码' type='password' v-model="formData.apwd"></el-input>
          </el-form-item> 
          <el-form-item>
            <el-button type="primary" @click.native="doLogin">登录</el-button>
            <el-button @click.native="doCancel">取消</el-button>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
  </div>
</template>
<script>
export default {
  data(){
    return{
      formData:{
        aname:'',
        apwd:''
      }
    }
  },
  methods: {
    doLogin(){//执行登录
      var data=this.formData;
      var url=this.$store.state.globalSettings.apiUrl+`/admin/login/${data.aname}/${data.apwd}`
      this.$axios.get(url).then(res=>{
        if(res.data.code==200){//登录成功
          //把用户名存入Vuex
          this.$store.commit('setAdminName',this.formData.aname);
          //跳转
          this.$router.push('/table/list')
        }else{//警告框 登录失败
          this.$alert('用户名或密码有误','登录失败',{type:'error'}).then(()=>{}).catch(()=>{});
        }
      }).catch(err=>{
        console.log(err);
      })
    },
    doCancel(){//清除用户输入
        this.formData.aname=''
        this.formData.apwd=''
    }
  }
}
</script>
<style lang="scss">
.login:before{
  content:'';
  display:table;
}
.login{
  background:url('../assets/timg.jpg') no-repeat fixed center;
  background-size:cover;
  height:100%;
}
.my-login-card{
  width: 450px;
  margin: 150px auto;
  .el-card__header {
    text-align: center;
  }
}

</style>