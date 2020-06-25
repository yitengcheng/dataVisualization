<template>
    <div class='container'>
        <div class='title'>
            <el-button class='map_button'>GIS地理资源展示</el-button>
            <div class="title_middle">
                <div class="query_box">
                    <PlainSelect label='区域' :pickerData="areaData"></PlainSelect>
                </div>
                <div class="query_box">
                    <PlainDatePick label='数据显示时间' type="month" format="yyyy年MM月"></PlainDatePick>
                </div>
                <el-button>查询</el-button>
            </div>
        </div>
        <div class='top'>
            <icon name="地图" class="map_box"></icon>
            <div class="community_box">
                <div class="community_box_top_data" >
                    <DataIcon v-for="(item,index) in communityBoxDatas" :key="index" :icon="item.icon" :value="item.value" :label="item.label"/>
                </div>
                <el-divider class="divider"></el-divider>
                <div class="community_box_bottom_data">
                    <div class="community_box_bottom_item">
                        <DataTitle title="社区治理" :datas="communityGovernance"/>
                    </div>
                    <div class="community_box_bottom_item">
                        <EchartsLineOrBar title="实有人口走访核对率" :option="visitData" value1="30%"/>
                    </div>
                    <div class="community_box_bottom_item">
                        <EchartsLineOrBar title="重点关注走访核对率" :option="focusOnData" value1="50%"/>
                    </div>
                    <div class="community_box_bottom_item">
                        <EchartsLineOrBar title="重点管控走访核对率" :option="keyToControlData" value1="100%" :isPass="true"/>
                    </div>
                    <div class="community_box_bottom_item" style="flexDirection:column">
                        <div class="community_box_bottom_item_info" v-for="(item,index) in houseUsage" :key="index">
                            <div class='community_box_bottom_item_info_title'>{{item.title}}</div>
                            <div class='community_box_bottom_item_info_data'>    
                                <div>使用：{{item.used}}</div>
                                <div>空置：{{item.empty}}</div>
                            </div>
                        </div>
                    </div>
                    <div class="community_box_bottom_item" style="flexDirection:column;flex:1">
                        <div class="community_box_bottom_item_text_info" v-for="(item, index) in communityInfoList" :key="index">
                            <div class="community_box_bottom_item_text_info_box" style="background-color:gray;color:#000">{{item.title}}</div>
                            <div class="community_box_bottom_item_text_info_box">共计：<br>{{item.total}}</div>
                            <div class="community_box_bottom_item_text_info_box">{{item.unfinishedTitle}}<br>{{item.unfinished}}</div>
                            <div class="community_box_bottom_item_text_info_box">{{item.completeTitle}}<span :class="[item.complete<0.6?'redText':item.complete>=0.6 && item.complete<0.8 ? 'orangeText':'greenText']">{{item.complete * 100}}%</span></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class='middle'></div>
        <div class='bottom'></div>
    </div>
</template>

<script>
import PlainSelect from '../components/plain/PlainSelect';
import PlainDatePick from '../components/plain/PlainDatePick';
import DataIcon from '../components/DataIcon';
import DataTitle from '../components/DataTitle';
import EchartsLineOrBar from '../components/EchartsLineOrBar';
export default {
    components:{PlainSelect,PlainDatePick,DataIcon,DataTitle,EchartsLineOrBar},
    data(){
        return { 
            areaData: ['明田街道'],
            communityBoxDatas:[
                {icon:'人口',value:'5465',label:'人口数量'},
                {icon:'房屋',value:'2465',label:'房屋数量'},
                {icon:'商业',value:'465',label:'商业机构'},
                {icon:'医疗',value:'15',label:'医疗机构'},
                {icon:'教育',value:'5',label:'教育机构'}
            ],
            communityGovernance:[
                {icon:'网格员',value:'7/15',label:'网格人员', w:".5rem" ,h:".5rem"},
                {icon:'管控人员',value:'265',label:'管控人员', w:".5rem" ,h:".5rem"},
                {icon:'关注人员',value:'246',label:'关注人员', w:".5rem" ,h:".5rem"},
                {icon:'事件',value:'1453',label:'上报事件', w:".5rem" ,h:".5rem"},
            ],
            visitData:{
                xAxis: {
                    type: 'category',
                    axisTick:{
                        "show":false
                    },
                    data: ['实有人口', '走访人口']
                },
                yAxis: {
                    show:false,
                    type: 'value'
                },
                grid: {
                    x: 10,
                    y: 0,
                    x2:10,
                    y2:20
                },
                series: [{
                    data: [5660, 2847],
                    type: 'bar',
                    barWidth:40,
                }]
            },
            focusOnData:{
                radar: {
                    name: {
                        textStyle: {
                            color: '#fff',
                            backgroundColor: '#999',
                            borderRadius: 3,
                            padding: [3, 5],
                            fontSize:8
                        }
                    },
                    nameGap : 1,
                    center:['50%','50%'], 
                    indicator: [
                        { name: '残疾', max: 90},
                        { name: '智障', max: 90},
                        { name: '留守儿童', max: 90},
                        { name: '空巢老人', max: 90},
                    ]
                },
                series: [{
                    type: 'radar',
                    data: [
                        {
                            value: [23,24,57,89],
                            name: '实际人员'
                        },
                        {
                            value: [15,24,55,89],
                            name: '走访人员'
                        }
                    ],
                }]
            },
            keyToControlData:{
                radar: {
                    name: {
                        textStyle: {
                            color: '#fff',
                            backgroundColor: '#999',
                            borderRadius: 3,
                            padding: [3, 5],
                            fontSize:8
                        }
                    },
                    nameGap : 1,
                    center:['50%','50%'], 
                    indicator: [
                        { name: '酗酒闹事', max: 90},
                        { name: '吸毒人员', max: 90},
                        { name: '刑事前科人员', max: 90},
                        { name: '精神病', max: 90},
                        { name: '闹访人员', max: 90},
                    ]
                },
                series: [{
                    type: 'radar',
                    data: [
                        {
                            value: [69,49,35,57,89],
                            name: '实际人员'
                        },
                        {
                            value: [60,46,34,55,89],
                            name: '走访人员'
                        }
                    ],
                }]
            },
            houseUsage:[
                {title:'房屋使用情况',used:'159',empty:'24'},
                {title:'铺面使用情况',used:'159',empty:'24'},
            ],
            communityInfoList:[
                {title:'人员信息变动异常',total:'12384',unfinishedTitle:'待核对：',unfinished:'965',completeTitle:'核对率：',complete:0.6},
                {title:'矛盾纠纷事件',total:'84',unfinishedTitle:'待调处：',unfinished:'14',completeTitle:'调处率：',complete:0.7},
                {title:'风险隐患事件',total:'56',unfinishedTitle:'待处理：',unfinished:'36',completeTitle:'完成率：',complete:0.45},
                {title:'居民诉求上报事件',total:'34',unfinishedTitle:'待处理：',unfinished:'2',completeTitle:'完成率：',complete:0.85},
            ]
        };
    }
    
};
</script>
<style lang='scss' scoped>
.container{
    display:flex;
    flex:1;
    flex-direction: column;
    background:url('../assets/bg.png') no-repeat center center;
}
.title {
    display: flex;
    height: 1rem;
    width:100%;
    flex-direction: row;
    align-items: center;
}
.map_button {
    height: .5rem;
    width: 2.5rem;
    color: red;
    font-size:12px;
    margin-left:20px;
}
.title_middle {
    display: flex;
    flex:1;
    justify-content: center;
}
.query_box{
    margin-right:40px;
}
.top {
    display: flex;
    flex:1.5;
    flex-direction: row;
}
.map_box {
    width: 4.43rem;
    height: 4.43rem;
}
.community_box {
    display: flex;
    flex:1;
    flex-direction: column;
}
.community_box_top_data{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content:space-around;
    padding-top: 10px;
}
.community_box_bottom_data {
    display: flex;
    flex-direction: row;
}
.community_box_bottom_item{
    display: flex;
    height: 2.75rem;
    width: 2.5rem;
    margin-right: 20px;
}
.community_box_bottom_item_info{
    display: flex;
    flex:1;
    flex-direction: column;
    border:1px solid gray;
    margin-bottom:5px;
    align-items:center;
    border-radius: 3px;
}
.community_box_bottom_item_info_title{
    background-color:gray;
    font-size:12px;
    width:100%;
    text-align:center;
    border-radius: 3px;
}
.community_box_bottom_item_info_data{
    display: flex;
    flex:1;
    flex-direction: column;
    justify-content: center;
    color: #fff;
}
.community_box_bottom_item_text_info{
    display: flex;
    flex-direction: row;
    align-items: space-around;
}
.community_box_bottom_item_text_info_box{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    flex:1;
    border:1px solid gray;
    border-radius: 5px;
    margin-top: 1px;
    margin-right: 5px;
    align-items: center;
    justify-content: center;
    padding: 0px 5px;
    color: #ffffff;
}
.redText{
    color:red
}
.orangeText{
    color:orange
}
.greenText{
    color:green
}
.divider{
    margin-top:10px;
    margin-bottom:10px;
}
.middle {
    display: flex;
    flex:1;
    background-color:green
}
.bottom {
    display: flex;
    flex:1;
    background-color:yellow
}
</style>
