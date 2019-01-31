<template>
    <div class="my-table-info">
        <el-card shadow="hover">
            <div class="my-table">
                {{data.tid}}号桌:{{data.stus | tableStatus}}
                {{data.tname}}            
            </div>
            <el-button type="success" plain>详情</el-button>
            <el-button type="danger" plain>修改</el-button>
        </el-card>
    </div>    
</template>
<script>
export default {
    props:['data']
}
</script>
<style lang="scss">
.my-table{
    width: 150px;
    height: 110px;
    background: greenyellow;
    border-radius: 50%;
    text-align: center;
    line-height: 110px;
}
</style>
