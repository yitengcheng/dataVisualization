<template>
    <div class='box'>
        <p class='title'>{{label+"："}}</p>
        <el-select v-for="(index,item) in pickerData"
        :key="index"
        :label="item"
        :value="index"></el-select>
    </div>
</template>

<script>
export default {
    props:{
        label:{
            type:String,
            default: "标题："
        },
        pickerData:{
            type:Array,
            default: ()=>{
                return [];
            }
        }
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
    color: #ffffff;
}
</style>