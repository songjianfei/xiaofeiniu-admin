<template>
  <div class="dishadd">
    <h3>添加菜品</h3>
    <el-form label-width="100px">
      <el-form-item label="菜品图片">
        <el-upload class="my-uploader" :action="uploadAction" :on-success="doUploadSucc" name="dishImg" :show-file-list="false">
          <img v-if="imgUrl" :src="imgUrl" alt="">
          <i v-else class="el-icon-plus upload-icon"></i>
        </el-upload>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      imgUrl:'',//要显示的预览图片地址
      uploadAction:this.$store.state.globalSettings.apiUrl+'/admin/dish/image',   //可处理文件上传的数据API
      formData:{
        title:'',
        imgUrl:'',
        price:'',
        detail:'',
        categoryId:''
      }
    }
  },
  methods: {
    doUploadSucc(res,file){
      //文件上传成功后，客户端得到响应消息之后的处理函数
      //res代表服务器端返回的响应消息
      //file:从INPUT[type=file]中读取的第一个上传文件对象
      this.formData.imgUrl=res.fileName;
      this.imgUrl=URL.createObjectURL(file.raw);
    }
  },
}
</script>
<style lang="scss">
.my-uploader .el-upload{
  border: 1px dashed #d9d9d9;
  border-radius: 6px;
  cursor: pointer;
  width: 250px;
  height: 177px;
  overflow: hidden;
  &:hover{
    border-color:#409EFF;
  }
  .upload-icon{
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
  }
}
</style>

