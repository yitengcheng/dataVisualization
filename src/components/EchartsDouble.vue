<template>
    <div class='box'>
        <div class='title'>{{title}}</div>
        <div class="echarts_box">
            <div class="echarts_box_left">
                <v-chart theme="light" class="echarts1" :options="option1"></v-chart>
                <div style="color:#72ACD1;fontSize:20px">{{value1}}</div>
            </div>
            <div class="echarts_box_right">
                <v-chart theme="light" class="echarts2" :options="option2"></v-chart>
                <div style="color:#72ACD1;fontSize:20px">{{value2}}</div>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    props:{
        title:{
            type:String,
            default:"标题"
        },
        option1:{
            type:Object,
            default:()=>{
                return {};
            }
        },
        option2:{
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
    flex:1;
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
.echarts_box {
    display: flex;
    flex:1;
    width:100%;
}
.echarts_box_left {
    display: flex;
    flex-direction: column;
    align-items: center;
    width:40%;
    height: 3rem;
    border-right: 1px solid gray;
}
.echarts_box_right {
    display: flex;
    flex-direction: column;
    align-items: center;
    width:60%;
    height: 3rem;
}
.echarts1 {
    width: 100%;
}
.echarts2 {
    width: 100%;
}
</style>