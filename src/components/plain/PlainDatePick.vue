<template>
    <div class='box'>
        <p class='title'>{{label+"："}}</p>
        <el-date-picker v-model="value" :format="format" :type="type"></el-date-picker>
    </div>
</template>

<script>
export default {
    props:{
        label:{
            type:String,
            default:"标题："
        },
        type:{
            type:String,
            default:"date"
        },
        format:{
            type:String,
            default:"yyyy-MM-dd"
        }
    },
    data(){
        return {
            value:''
        };
    }
};
</script>
<style lang='scss' scoped>
.box {
    display: flex;
    flex-direction: row;
    align-items: center;
}
.title {
    font-size:18px;
    color:#ffffff;
}
</style>