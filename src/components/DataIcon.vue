<template>
    <div class='box'>
        <icon :w="w" :h="h" :name="icon"/>
        <div :class="[label.length<=4 ? 'box_label': 'box_label_large']">{{label}}</div>
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
    font-size:18px;
    color:#fff;
    margin: 0px 5px;
}
.box_label_large{
    display: flex;
    flex-wrap: wrap;
    width:.8rem;
    font-size:16px;
    color:#fff;
    margin: 0px 5px;
}
.box_value {
    font-size: 24px;
    font-weight: 700;
    color:#fff;
}
</style>