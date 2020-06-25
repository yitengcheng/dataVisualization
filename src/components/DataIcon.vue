<template>
    <div class='box'>
        <icon :w="w" :h="h" :name="icon"/>
        <div class="box_label">{{label}}</div>
        <div class="box_value">{{value}}</div>
    </div>
</template>

<script>
export default {
    components: {},
    props:{
        icon:{
            type: String,
            default:"默认"
        },
        value:{
            type: String,
            default:"0"
        },
        label:{
            type: String,
            default:"标题"
        },
        w:{
            type: String,
            default:".75rem"
        },
        h:{
            type: String,
            default:".75rem"
        }

    },
};
</script>
<style lang='scss' scoped>
.box {
    display: flex;
    flex-direction: row;
    align-items: flex-end;
}
.box_label{
    display: flex;
    flex-wrap: wrap;
    width:.5rem;
    font-size:14px;
    color:#fff;
    margin: 0px 5px;
}
.box_value {
    font-size: 18px;
    font-weight: 700;
    color:#fff;
}
</style>