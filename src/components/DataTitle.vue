<template>
    <div class='box'>
        <div class='title'>{{title}}</div>
        <div class='data_icon_box'>
            <DataIcon v-for="(item,index) in datas" :key="index" 
            :icon="item.icon" :value="item.value" :label="item.label" :w="item.w" :h="item.h"/>
        </div>
    </div>
</template>

<script>
import DataIcon from './DataIcon';
export default {
    components: {DataIcon},
    props:{
        title:{
            type: String,
            default:"标题"
        },
        datas:{
            type:Array,
            default:()=>{
                return [];
            }
        }
    },
};
</script>
<style lang='scss' scoped>
.box {
    display: flex;
    flex:1;
    flex-direction: row;
    align-items: center;
}
.title {
    display: flex;
    padding: 10px;
    width:.25rem;
    height: 2.5rem;
    align-items: center;
    font-size:20px;
    background-color:gray;

}
.data_icon_box {
    display: flex;
    flex-direction: column;
    height: 2.75rem;
    justify-content: space-around;
    margin-left: 10px;
}
</style>