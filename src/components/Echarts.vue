<template>
    <div class='box'>
        <div class='title'>{{title}}</div>
        <v-chart theme="light" class="echarts" :options="option"></v-chart>
        <div style="color:#fff;fontSize:20px"><span style="color:red">{{value1}}</span>/{{value2}}</div>
        <div v-if="isShowBottom" :class="[isPass?'pass':'no_pass']">{{isPass ? '达标':'未达标'}}</div>
    </div>
</template>

<script>
export default {
    props:{
        title:{
            type:String,
            default:"标题"
        },
        option:{
            type:Object,
            default:()=>{
                return {};
            }
        },
        value1:{
            type:String,
            default:"0%",
        },
        value2:{
            type:String,
            default:"100%",
        },
        isPass:{
            type:Boolean,
            default:false,
        },
        isShowBottom:{
            type:Boolean,
            default:true,
        }
    },
};
</script>
<style lang='scss' scoped>
.box {
    display: flex;
    width: 100%;
    flex-direction: column;
    align-items: center;
    border:0.5px solid gray;
    border-radius: 3px;
}
.title {
    background-color:gray;
    font-size:14px;
    width:100%;
    text-align:center;
    border-radius: 3px;
}
.echarts {
    width: 100%;
}
.no_pass{
    width: 2rem;
    background-color:orange;
    text-align: center;
    border-radius: 5px;
    margin-bottom: 5px;
}
.pass{
    width: 2rem;
    background-color:green;
    text-align: center;
    border-radius: 5px;
    margin-bottom: 5px;
}
</style>