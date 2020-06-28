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
            <img class='map_box' src='../assets/shequ_lan.png'/>
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
                        <Echarts title="实有人口走访核对率" :option="visitData" value1="30%"/>
                    </div>
                    <div class="community_box_bottom_item">
                        <Echarts title="重点关注走访核对率" :option="focusOnData" value1="50%"/>
                    </div>
                    <div class="community_box_bottom_item">
                        <Echarts title="重点管控走访核对率" :option="keyToControlData" value1="100%" :isPass="true"/>
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
                            <div class="community_box_bottom_item_text_info_box" style="background-color:gray;color:#000;">{{item.title}}</div>
                            <div class="community_box_bottom_item_text_info_box">共计：<br>{{item.total}}</div>
                            <div class="community_box_bottom_item_text_info_box">{{item.unfinishedTitle}}<br>{{item.unfinished}}</div>
                            <div class="community_box_bottom_item_text_info_box">{{item.completeTitle}}<span :class="[item.complete<0.6?'redText':item.complete>=0.6 && item.complete<0.8 ? 'orangeText':'greenText']">{{item.complete * 100}}%</span></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <el-divider class="divider"></el-divider>
        <div class='middle'>
            <div class="middle_item">
                <DataTitle title="培训就业" :datas="trainingBoxDatas"/>
            </div>
            <div class="middle_item">
                <Echarts title="就业率" :option="employmentRate" value1="80%" value2="90%" :isShowBottom="false"/>
            </div>
            <div class="middle_item" style="margin-right:20px;">
                <Echarts title="外出务工情况" :option="workOutsideRate" value1="42%" value2="58%" :isShowBottom="false"/>
            </div>
            <div class="middle_item" style="margin-right:20px;">
                <Echarts title="智能匹配本地就业率" :option="matchTheJobsDatas" value1="90%" value2="" :isShowBottom="false"/>
            </div>
            <div class="middle_item_double" style="margin-right:20px;">
                <EchartsDouble title="本地企业差额用工情况" :option1="lackPropleInfoData" value1="差额人员200" :option2="lackPeopleData" value2="差额技能人员200"/>
            </div>
            <div class="middle_item" style="width:5rem;margin-right:20px;">
                <Echarts title="待业原因情况" :option="unemploymentReason" value1="待核查人数：41" value2="已核查人数：159" :isShowBottom="false"/>
            </div>
        </div>
        <el-divider class="divider"></el-divider>
        <div class='bottom'>
            <div class="bottom_box">
                <div class="bottom_box_title">公共服务</div>
                <div style="display:flex;flex:1;align-items: center;justify-content:center;font-size:20px;color:#ffffff;">建设中</div>
            </div>
            <div class="bottom_box">
                <div class="bottom_box_title">文化服务</div>
                <div style="display:flex;flex:1;align-items: center;justify-content:center;font-size:20px;color:#ffffff;">建设中</div>
            </div>
            <div class="bottom_box">
                <div class="bottom_box_title">基层党建</div>
                <div style="display:flex;flex:1;align-items: center;justify-content:center;font-size:20px;color:#ffffff;">建设中</div>
            </div>
        </div>
    </div>
</template>

<script>
import PlainSelect from '../components/plain/PlainSelect';
import PlainDatePick from '../components/plain/PlainDatePick';
import DataIcon from '../components/DataIcon';
import DataTitle from '../components/DataTitle';
import Echarts from '../components/Echarts';
import EchartsDouble from '../components/EchartsDouble';
export default {
    components:{PlainSelect,PlainDatePick,DataIcon,DataTitle,Echarts,EchartsDouble},
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
                    axisLabel: {
                        color: '#ffffff'
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
                            name: '实际人员',
                            areaStyle: {
                                normal: {
                                    color: '#72ACD1'
                                }
                            }
                        },
                        {
                            value: [15,24,55,89],
                            name: '走访人员', 
                            areaStyle: {
                                normal: {
                                    color: '#72ACD1'
                                }
                            }
                        }
                    ],
                }]
            },
            keyToControlData:{
                radar: {
                    name: {
                        textStyle: {
                            color: '#fff',
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
                            name: '实际人员',
                            areaStyle: {
                                normal: {
                                    color: '#72ACD1'
                                }
                            }
                        },
                        {
                            value: [60,46,34,55,89],
                            name: '走访人员',
                            areaStyle: {
                                normal: {
                                    color: '#72ACD1'
                                }
                            }
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
            ],
            trainingBoxDatas:[
                {icon:'劳动力',value:'2465',label:'具备劳动力人数', w:".5rem" ,h:".5rem"},
                {icon:'不具备劳动力',value:'465',label:'不具备劳动力人数', w:".5rem" ,h:".5rem"},
                {icon:'企业',value:'500',label:'企业需求用工数量', w:".5rem" ,h:".5rem"},
                {icon:'待业',value:'200',label:'待业人员数量', w:".5rem" ,h:".5rem"},
            ],
            employmentRate:{
                title: [{
                    text: '2465',
                    top: 'center',
                    left: 'center',
                    textStyle: {
                        color:'#fff'
                    }
                }],
                series: [{
                    type: 'pie',
                    radius: ['30%', '70%'],
                    center: ['50%', '50%'],
                    data: [{
                        name: "就业",
                        value: "5660"
                    },
                    {
                        name: "待业",
                        value: "2598"
                    }],
                    label:{
                        normal:{
                            show:true,
                            position:'inner', //标签的位置
                            textStyle : {
                                fontWeight : 300 ,
                                fontSize : 14
                            },
                            formatter:'{c}'
                        }
                    },
                }]
            },
            workOutsideRate:{
                title: [{
                    text: '1465',
                    top: 'center',
                    left: 'center',
                    textStyle: {
                        color:'#fff'
                    }
                }],
                series: [{
                    type: 'pie',
                    radius: ['30%', '70%'],
                    center: ['50%', '50%'],
                    data: [{
                        name: "本地就业",
                        value: "1300"
                    },
                    {
                        name: "外出就业",
                        value: "890"
                    }],
                    label:{
                        normal:{
                            show:true,
                            position:'inner', //标签的位置
                            textStyle : {
                                fontWeight : 300 ,
                                fontSize : 14
                            },
                            formatter:'{d}%'
                        }
                    },
                }]
            },
            matchTheJobsDatas:{
                radar: {
                    name: {
                        textStyle: {
                            color: '#fff',
                            borderRadius: 3,
                            padding: [3, 5],
                            fontSize:8
                        }
                    },
                    nameGap : 1,
                    center:['50%','50%'], 
                    indicator: [
                        { name: '养殖', max: 140},
                        { name: '种植', max: 140},
                        { name: '建筑', max: 140},
                        { name: '家政服务', max: 140},
                        { name: '畅饮服务', max: 140},
                        { name: '销售', max: 140},
                        { name: '会计', max: 140},
                    ]
                },
                series: [{
                    type: 'radar',
                    data: [
                        {
                            value: [69,58,78,68,86,74,23],
                            name: '企业需求人员',
                        },
                        {
                            value: [56,46,126,34,66,34,12],
                            name: '待业技能人员', 
                        }
                    ],
                }]
            },
            lackPeopleData:{
                xAxis: {
                    type: 'category',
                    axisTick:{
                        "show":false
                    },
                    axisLabel: {
                        color: '#ffffff',
                        fontSize:8,
                        rotate: 20,
                    },
                    data: ['养殖', '种植','建筑','家政服务', '畅饮服务', '销售', '会计']
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
                    data: [56,46,126,34,66,34,12],
                    type: 'bar',
                    barWidth:20,
                }]
            },
            lackPropleInfoData:{
                xAxis: {
                    type: 'category',
                    axisTick:{
                        "show":false
                    },
                    axisLabel: {
                        color: '#ffffff'
                    },
                    data: ['所需人员', '待业人员']
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
                    data: [456, 256],
                    type: 'bar',
                    barWidth:40,
                }]
            },
            unemploymentReason:{
                grid: {
                    x: 80,
                    y: 10,
                    x2:10,
                    y2:10
                },
                yAxis: [{
                    type: 'category',
                    data: ['没有技能','照顾家人','生病','找不到工作','自由职业'],
                    inverse: true,
                    axisTick: {
                        alignWithLabel: true,
 
 
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 10,
                            color: 'white'
                        }
                    },
                }],
                xAxis: {show: false},
                series: [{
                    name: 'Top 10',
                    type: 'bar',
                    barWidth: 26,
                    data: [39,23,14,56,34],
                    label: {
                        normal: {
                            show: true,
                            position: 'insideRight',
                            textStyle: {
                                color: '#fff', //color of value
                                fontSize: 14,
                            }
                        }
                    }
                }]
            }
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
    overflow: hidden;
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
    width:100%;
    height: 4.43rem;
    align-items: center;
    flex-direction: row;
}
.map_box {
    width: 4.43rem;
    height: 4.43rem;
}
.community_box {
    display: flex;
    height: 4.43rem;
    width:100%;
    flex-direction: column;
    justify-content: center;
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
    height: 3.25rem;
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
    font-size:14px;
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
    font-size:18px;
}
.community_box_bottom_item_text_info{
    display: flex;
    flex-direction: row;
    align-items: space-around;
    flex-wrap: wrap;
}
.community_box_bottom_item_text_info_box{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    flex:1;
    min-height:.75rem;
    border:1px solid gray;
    border-radius: 5px;
    margin-top: 1px;
    margin-right: 5px;
    align-items: center;
    justify-content: center;
    padding: 0px 5px;
    color: #ffffff;
    font-size: 22px;
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
    margin:10px 0px;
}
.middle {
    display: flex;
    width:100%;
    height: 4.43rem;
    align-items: center;
    flex-direction: row;
}
.middle_item {
    display: flex;
    height:3.25rem;
    width: 3rem;
}
.middle_item_double{
    display: flex;
    height: 3.25rem;
    width: 6rem;
}
.bottom {
    display: flex;
    width:100%;
    height: 4.43rem;
    align-items: center;
    flex-direction: row;
}
.bottom_box {
    display: flex;
    flex-direction: row;
    width:33%;
    height: 3rem;
}
.bottom_box_title {
    display: flex;
    padding: 10px;
    width:.25rem;
    height: 2.5rem;
    align-items: center;
    font-size:20px;
    background-color:gray;
}
</style>
