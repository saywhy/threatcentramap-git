<template>
    <el-row :gutter="10">
        <!-- 左边 -->
        <el-col :xs="7" :sm="7" :md="7" :lg="7" :xl="7">
            <div class="grid_content bg_left">
                <!-- 左上 -->
                <div class="bg_left_top">
                    <p>威胁告警分布</p>
                    <div class="bg_left_level">
                        <el-row :gutter="0">
                            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
                                <div id="threat_alarm_left">
                                </div>
                            </el-col>
                            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
                                <div id="threat_alarm_right">
                                </div>
                            </el-col>
                        </el-row>
                    </div>
                </div>
                <!-- 左中 -->
                <div class="bg_left_mid ">
                    <p>重点关注告警类型</p>
                    <div class="bg_left_mid_item" style="margin-top:40px;">
                        <el-row :gutter="0">
                            <el-col :xs="4" :sm="4" :md="4" :lg="4" :xl="4">
                                <span v-text="alarmTypeData[0].fName"></span>
                            </el-col>
                            <el-col :xs="18" :sm="18" :md="18" :lg="18" :xl="18">
                                <div id="alarm_type_f"></div>
                            </el-col>
                            <el-col :xs="2" :sm="2" :md="2" :lg="2" :xl="2">
                                <span v-text="alarmTypeData[0].fNum"></span>
                            </el-col>
                        </el-row>
                    </div>
                    <div class="bg_left_mid_item">
                        <el-row :gutter="0">
                            <el-col :xs="4" :sm="4" :md="4" :lg="4" :xl="4">
                                <span v-text="alarmTypeData[0].sName"></span>
                            </el-col>
                            <el-col :xs="18" :sm="18" :md="18" :lg="18" :xl="18">
                                <div id="alarm_type_s"></div>
                            </el-col>
                            <el-col :xs="2" :sm="2" :md="2" :lg="2" :xl="2">
                                <span v-text="alarmTypeData[0].sNum"></span>
                            </el-col>
                        </el-row>
                    </div>
                    <div class="bg_left_mid_item" style="margin-bottom:20px">
                        <el-row :gutter="0">
                            <el-col :xs="4" :sm="4" :md="4" :lg="4" :xl="4">
                                <span v-text="alarmTypeData[0].tName"></span>
                            </el-col>
                            <el-col :xs="18" :sm="18" :md="18" :lg="18" :xl="18">
                                <div id="alarm_type_t"></div>
                            </el-col>
                            <el-col :xs="2" :sm="2" :md="2" :lg="2" :xl="2">
                                <span v-text="alarmTypeData[0].tNum"></span>
                            </el-col>
                        </el-row>
                    </div>
                    <el-table :data="alarmTypeData" style="width: 100%;" :show-overflow-tooltip="true" :row-style="tableRowStyle" :header-cell-style="HeaderColor">
                        <el-table-column prop="name" label="" :show-overflow-tooltip="true">
                        </el-table-column>
                        <el-table-column prop="fNum" :label="alarmTypeData[0].fName" :show-overflow-tooltip="true">
                        </el-table-column>
                        <el-table-column prop="sNum" :label="alarmTypeData[0].sName" :show-overflow-tooltip="true">
                        </el-table-column>
                        <el-table-column prop="tNum" :label="alarmTypeData[0].tName" :show-overflow-tooltip="true">
                        </el-table-column>
                    </el-table>
                </div>
                <!-- 左下 -->
                <div class="bg_left_bom ">
                    <p>风险趋势</p>
                    <div id="disk_trend"></div>
                </div>
            </div>
        </el-col>
        <!-- 中间 -->
        <el-col :xs="10" :sm="10" :md="10" :lg="10" :xl="10">
            <div class="grid_content bg_mid">
                <div class="bg_mid_top">
                    <div id="china_map"></div>
                </div>
                <div class="bg_mid_bom">
                    <el-row :gutter="0">
                        <el-col :xs="14" :sm="14" :md="14" :lg="14" :xl="14">
                            <el-row :gutter="0">
                                <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
                                    <p>实时情报更新</p>
                                </el-col>
                                <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
                                    <p>实时威胁告警</p>
                                </el-col>

                            </el-row>
                            <div>
                                <img src="../assets/img/123.jpg" alt="" class="bg_mid_bom_img">
                            </div>
                        </el-col>
                        <el-col :xs="10" :sm="10" :md="10" :lg="10" :xl="10">
                            <p>信息扩展和关联</p>
                            <div id="info_relation">
                            </div>
                        </el-col>
                    </el-row>
                </div>
            </div>
        </el-col>
        <!-- 右边 -->
        <el-col :xs="7" :sm="7" :md="7" :lg="7" :xl="7">
            <div class="grid_content bg_right">
                <div class="bg_right_top">
                    <p>二级公司威胁态势</p>
                    <div class="bg_right_top_item">
                        <el-row :gutter="0" class="bg_right_top_row" v-for="item in companyThreat">
                            <el-col :xs="5" :sm="5" :md="5" :lg="5" :xl="5">
                                <span class="bg_right_top_span" v-text="item.name"></span>
                                <span class="bg_right_top_span" v-text="item.num"></span>
                            </el-col>
                            <el-col :xs="18" :sm="18" :md="18" :lg="18" :xl="18">
                                <p class="bg_right_top_row_p">
                                    <span class="bg_right_top_row_span1" :style="item.high"></span>
                                    <span class="bg_right_top_row_span2" :style="item.mid"></span>
                                    <span class="bg_right_top_row_span3" :style="item.low"></span>
                                </p>
                            </el-col>
                        </el-row>
                    </div>

                </div>
                <div class="bg_right_mid">
                    <p>攻击点威胁排行</p>
                    <el-table :data="tableData" style="width: 100%;" :show-overflow-tooltip="true" :row-style="tableRowStyle" :header-cell-style="tableHeaderColor">
                        <el-table-column prop="ip" label="攻击点" :show-overflow-tooltip="true">
                        </el-table-column>
                        <el-table-column prop="type" label="类型" :show-overflow-tooltip="true">
                        </el-table-column>
                        <el-table-column prop="num" label="威胁数量" :show-overflow-tooltip="true">
                            <p>
                            </p>
                        </el-table-column>
                        <el-table-column prop="src" label="归属" :show-overflow-tooltip="true">
                        </el-table-column>
                    </el-table>
                </div>
                <div class="bg_right_bom">
                    <p>全球安全动态</p>
                    <ul style="padding-left:20px">
                        <li class="bg_right_bom_li">
                            <p class="bg_right_bom_title">所有英特尔处理器面临新的Spoiler攻击</p>
                            <p class="bg_right_bom_time">7小时前</p>
                        </li>
                        <li class="bg_right_bom_li">
                            <p class="bg_right_bom_title">微软安全报告显示去年网络钓鱼攻击有所增加</p>
                            <p class="bg_right_bom_time">10小时前</p>
                        </li>
                        <li class="bg_right_bom_li">
                            <p class="bg_right_bom_title">RSA 2019| Axonius 获得创新沙盒冠军</p>
                            <p class="bg_right_bom_time">一天前</p>
                        </li>
                        <li class="bg_right_bom_li">
                            <p class="bg_right_bom_title">‘Ji32k7au4a’ 被发现是一个令人惊讶的糟糕密码</p>
                            <p class="bg_right_bom_time">一周前</p>
                        </li>
                    </ul>
                </div>
            </div>
        </el-col>
    </el-row>
</template>
<style scoped  lang="less">
.el-col {
  border-radius: 4px;
  .grid_content {
    border-radius: 4px;
    min-height: 980px;
  }
  // 左边
  .bg_left {
    background: rgba(6, 33, 65, 0.5);
    border-radius: 5px;
    p {
      height: 30px;
    }
    //   左上
    .bg_left_top {
      border: 1px solid #0f2767;
      border-radius: 5px;
      padding-top: 20px;
      height: 250px;
      margin-bottom: 30px;
      .bg_left_level {
        #threat_alarm_left {
          padding-top: 10px;
          height: 200px;
          //   border: 1px solid red;
        }
        #threat_alarm_right {
          padding-top: 10px;
          height: 200px;
          //   border: 1px solid red;
        }
      }
    }
    //   左中
    .bg_left_mid {
      border: 1px solid #0f2767;
      border-radius: 5px;
      height: 330px;
      padding-top: 10px;
      margin-bottom: 20px;
      .bg_left_mid_item {
        margin: 5px;
        height: 30px;
        //   border: 1px solid red;
        line-height: 30px;
        #alarm_type_f,
        #alarm_type_s,
        #alarm_type_t {
          // border: 1px solid red;
          height: 30px;
          width: 100%;
        }
      }
      .el-table {
        color: #fff;
        background-color: rgba(6, 33, 65, 0) !important;
        border-radius: 3px;
      }
      .el-table th,
      .el-table tr {
        background-color: rgba(6, 33, 65, 0);
      }
      .el-table--enable-row-hover .el-table__body tr:hover > td {
        background-color: rgba(65, 6, 26, 0.65) !important;
      }
      .el-table td,
      .el-table th.is-leaf {
        border-bottom: 1px solid #0f2767;
        text-align: center;
        font-size: 10px;
      }
      .el-table--border::after,
      .el-table--group::after,
      .el-table::before {
        content: "";
        position: absolute;
        background-color: #ebeef5;
        z-index: -1;
      }
    }
    //   左下
    .bg_left_bom {
      padding: 10px;
      border: 1px solid #0f2767;
      height: 340px;
      p {
        height: 30px;
      }
      #disk_trend {
        height: 300px;
      }
    }
  }
  // 中间
  .bg_mid {
    p {
      height: 30px;
    }
    .bg_mid_top {
      border: 1px solid #0f2767;
      height: 610px;
      padding-top: 30px;
      margin-bottom: 20px;
      background: rgba(6, 33, 65, 0.5);
      #china_map {
        height: 580px;
      }
    }
    .bg_mid_bom {
      border: 1px solid #0f2767;
      background: rgba(6, 33, 65, 0.5);
      height: 340px;
      padding-top: 10px;
      #info_relation {
        //   border: 1px solid red;
        height: 300px;
      }
      .bg_mid_bom_img {
        width: 100%;
        height: 300px;
      }
    }
  }
  // 右边
  .bg_right {
    background: rgba(6, 33, 65, 0.5);
    border-radius: 5px;
    .bg_right_top {
      border: 1px solid #0f2767;
      border-radius: 5px;
      padding-top: 20px;
      height: 250px;
      margin-bottom: 30px;
      .bg_right_top_item {
        padding: 5px;
        .bg_right_top_row {
          margin: 10px 5px;
          .bg_right_top_span {
            font-size: 10px;
          }

          .bg_right_top_progress {
            margin-top: 8px;
          }
          .bg_right_top_row_p {
            width: 100%;
            height: 5px;
            line-height: 20px;
            border-radius: 5px;
            margin: 8px 0;
            background: #fff;
            .bg_right_top_row_span1 {
              float: left;
              width: 20%;
              height: 100%;
              background: rgba(150, 33, 22, 0.6);
              border-radius: 5px;
            }
            .bg_right_top_row_span2 {
              margin-left: -2px;
              float: left;
              width: 40%;
              height: 100%;
              border-radius: 5px;
              background: rgba(245, 191, 65, 0.8);
            }
            .bg_right_top_row_span3 {
              margin-left: -2px;
              float: left;
              width: 15%;
              height: 100%;
              border-radius: 5px;
              background: rgba(74, 164, 110, 0.8);
            }
          }
        }
      }
    }
    .bg_right_mid {
      border: 1px solid #0f2767;
      border-radius: 5px;
      padding-top: 10px;
      height: 330px;
      margin-bottom: 20px;
      p {
        height: 30px;
      }
      .el-table {
        color: #fff;
        background-color: rgba(6, 33, 65, 0.9) !important;
        border-radius: 3px;
      }
      .el-table th,
      .el-table tr {
        background-color: rgba(6, 33, 65, 0.9);
      }
      .el-table--enable-row-hover .el-table__body tr:hover > td {
        background-color: rgba(65, 6, 26, 0.65) !important;
      }
      .el-table td,
      .el-table th.is-leaf {
        border-bottom: 1px solid #0f2767;
        text-align: center;
        font-size: 10px;
      }
      .el-table--border::after,
      .el-table--group::after,
      .el-table::before {
        content: "";
        position: absolute;
        background-color: #ebeef5;
        z-index: -1;
      }
    }
    //   右下
    .bg_right_bom {
      padding: 10px;
      border: 1px solid #0f2767;
      height: 340px;
      overflow: hidden;
      p {
        height: 30px;
        margin-bottom: 20px;
      }
      // .el-carousel__item p {
      //   font-size: 14px;
      //   opacity: 0.75;
      //   //   line-height: 300px;
      //   margin: 0;
      // }
      .bg_right_bom_li {
        text-align: left;
        list-style: disc;
        margin: 0px;
        //   background: rgba(42, 102, 152, 0.2);
        padding: 9px 5px 4px 10px;
        border-radius: 5px;

        p {
          height: 26px;
        }
        .bg_right_bom_title {
          font-size: 14px;
          margin: 0;
        }
        .bg_right_bom_time {
          font-size: 10px;
          margin: 0;
          color: #d3d3d3;
        }
      }
    }
  }
}
</style>

<script>
export default {
    name: 'e-map',
    data() {
        return {
            tableData: [{
                ip: '192.168.1.2',
                type: '资产类型',
                num: '221',
                src: '二级公司'
            }, {
                ip: 'WWW.BAODE.COM',
                type: '资产类型',
                address: '北京市',
                num: '124',
                src: '二级公司'
            }, {
                ip: '47.23.123.31',
                type: '资产类型',
                num: '122',
                src: '二级公司'
            }, {
                ip: '78.24.61.195',
                type: '资产类型',
                num: '112',
                src: '二级公司'
            }, {
                ip: 'WWW.BAIDUSW.COM',
                type: '资产类型',
                num: '97',
                src: '二级公司'
            }
            ],
            tableDataProgress: [{ high: 212, mid: 32, low: 12 }, { high: 212, mid: 32, low: 12 }, { high: 212, mid: 32, low: 12 }, { high: 212, mid: 32, low: 12 }],
            alarmTypeData: [
                {
                    name: '影响资产数',
                    fName: '数据泄露',
                    sName: '勒索软件',
                    tName: '高危漏洞',
                    fNum: 123,
                    sNum: 2332,
                    tNum: 12213,
                }
            ],
            companyThreat: [
                {
                    name: '福建',
                    num: '5233',
                    high: 'width:30%',
                    mid: 'width:10%',
                    low: 'width:40%'
                }, {
                    name: '天津',
                    num: '4178',
                    high: 'width:20%',
                    mid: 'width:20%',
                    low: 'width:20%'
                }, {
                    name: '上海',
                    num: '4022',
                    high: 'width:10%',
                    mid: 'width:30%',
                    low: 'width:15%'
                }, {
                    name: '北京',
                    num: '2333',
                    high: 'width:8%',
                    mid: 'width:23%',
                    low: 'width:20%'
                }, {
                    name: '大连',
                    num: '1233',
                    high: 'width:5%',
                    mid: 'width:32%',
                    low: 'width:8%'
                }, {
                    name: '黑龙江',
                    num: '233',
                    high: 'width:4%',
                    mid: 'width:12%',
                    low: 'width:20%'
                }
            ],
            items: [
                {
                    type: ' Docker API和社区图像被用于传播挖矿软件',
                    address: 'Adobe发布更新修补ColdFusion中0day漏洞',
                    num: ' 安全厂商披露新Golang僵尸网络GoBrust',
                    name: 'Necurs僵尸网络采用新政策逃避检测'
                },
                {
                    type: ' Docker API和社区图像被用于传播挖矿软件',
                    address: '111111',
                    num: ' 111111',
                    name: '11111111111'
                },
                {
                    type: ' Adobe发布更新修补ColdFusion中0day漏洞',
                    address: '22222222',
                    num: ' 2222222',
                    name: '22222222'
                },
                {
                    type: '安全厂商披露新Golang僵尸网络GoBrust',
                    address: '333',
                    num: ' 3333',
                    name: '33333'
                },
                {
                    type: 'Necurs僵尸网络采用新政策逃避检测',
                    address: '44444',
                    num: ' 4444444',
                    name: '444444'
                },
            ],
            setindex: 0
        }
    },
    mounted() {
        // 左上
        this.threat_alarm_left_echarts();
        this.threat_alarm_right_echarts();
        // 左中
        this.alarm_type_f_echarts();
        this.alarm_type_s_echarts();
        this.alarm_type_t_echarts();
        this.disk_trend_echarts();
        this.info_relation_echarts();
    },
    methods: {
        // 左上
        threat_alarm_left_echarts() {
            var mychart = echarts.init(document.getElementById("threat_alarm_left"));
            var option = {
                title: {
                    text: '威胁等级分布',
                    x: '15%',
                    align: 'center',
                    top: 0,
                    verticalAlign: 'top',
                    textStyle: {
                        fontSize: 14,
                        color: '#fff'
                    }
                },
                legend: {
                    orient: 'vertical',
                    right: -5,
                    top: 20,
                    // left: 'center',
                    textStyle: {
                        color: '#fff',
                        fontSize: 10
                    },
                    data: ['高危', '中危', '低危']
                },
                color: ['rgba(150,33,22,.8)', 'rgba(245,191,65,.8)', 'rgba(74,164,110,.8)'],
                series: [
                    {
                        name: '',
                        type: 'pie',
                        radius: ['40%', '60%'],
                        center: ['40%', '60%'],
                        avoidLabelOverlap: false,
                        hoverAnimation: false,//是否开启 hover 在扇区上的放大动画效果。
                        legendHoverLink: false,//是否启用图例 hover 时的联动高亮。
                        label: {
                            normal: {
                                show: false,
                                position: 'center'
                            },
                            emphasis: {
                                show: true,
                                textStyle: {
                                    fontSize: '20',
                                    fontWeight: 'bold'
                                }
                            }
                        },
                        labelLine: {
                            normal: {
                                show: false
                            }
                        },
                        data: [
                            { value: 335, name: '高危' },
                            { value: 310, name: '中危' },
                            { value: 234, name: '低危' },
                        ]
                    }
                ]
            };
            mychart.setOption(option, true);
        },
        threat_alarm_right_echarts() {
            var mychart = echarts.init(document.getElementById("threat_alarm_right"));
            var option = {
                title: {
                    text: '威胁类型分布',
                    x: '10%',
                    align: 'center',
                    top: 0,
                    verticalAlign: 'top',
                    textStyle: {
                        fontSize: 14,
                        color: '#fff'
                    }
                },
                legend: {
                    orient: 'vertical',
                    right: -5,
                    top: 20,
                    // left: 'center',
                    textStyle: {
                        color: '#fff',
                        fontSize: 10
                    },
                    data: ['恶意IP', '僵尸网络', '恶意程序', '垃圾邮件']
                },
                // tooltip: {
                //     trigger: 'item',
                //     formatter: "{a} <br/>{b}: {c} ({d}%)"
                // },
                series: [{
                    name: '',
                    type: 'pie',
                    radius: ['40%', '60%'],
                    center: ['30%', '60%'],
                    hoverAnimation: false,//是否开启 hover 在扇区上的放大动画效果。
                    legendHoverLink: false,//是否启用图例 hover 时的联动高亮。
                    avoidLabelOverlap: false,
                    label: {
                        normal: {
                            show: false,
                            position: 'center'
                        },
                        emphasis: {
                            show: true,
                            textStyle: {
                                fontSize: '16',
                                fontWeight: 'bold'
                            }
                        }
                    },
                    labelLine: {
                        normal: {
                            show: false
                        }
                    },
                    data: [
                        { value: 335, name: '恶意IP' },
                        { value: 310, name: '僵尸网络' },
                        { value: 234, name: '恶意程序' },
                        { value: 135, name: '垃圾邮件' }
                    ]
                }
                ]
            };
            mychart.setOption(option, true);

        },
        // 左中
        alarm_type_f_echarts() {
            var mychart = echarts.init(document.getElementById("alarm_type_f"));
            var option = {
                grid: {
                    left: 5, top: 2, bottom: 8, right: 5,
                },
                xAxis: {
                    type: 'category',
                    data: ['02.18', '02.19', '02.20', '02.21', '02.22', '02.23', '02.24', '02.25', '02.26', '02.27', '02.28', '02.29', '02.30', '02.31'],
                    boundaryGap: false,
                    splitLine: {
                        show: true,
                        interval: 'auto',
                        lineStyle: {
                            color: ['#D4DFF5']
                        }
                    },
                    axisTick: {
                        show: false
                    },
                    splitLine: {
                        show: false
                    },
                    axisLine: {
                        show: false
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 14
                        }
                    }
                },
                yAxis: {
                    type: 'value',
                    splitLine: {
                        show: false
                    },
                    axisTick: {
                        show: false
                    },
                    axisLine: {
                        show: false
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 14
                        }
                    }
                },
                series: [{
                    name: '',
                    type: 'line',
                    smooth: true,
                    showSymbol: false,
                    symbol: 'circle',
                    symbolSize: 2,
                    data: ['200', '400', '888', '781', '926', '288', '300', '200', '400', '888', '781', '926', '288', '300'],
                    areaStyle: {
                        normal: {
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                offset: 0,
                                color: '#f7b851'
                            }, {
                                offset: 1,
                                color: '#f7b851'
                            }], false)
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: '#f7b851'
                        }
                    },
                    lineStyle: {
                        normal: {
                            width: 1
                        }
                    }
                }]
            };
            mychart.setOption(option, true);
        },
        alarm_type_s_echarts() {
            var mychart = echarts.init(document.getElementById("alarm_type_s"));
            var option = {
                grid: {
                    left: 5, top: 2, bottom: 8, right: 5,
                },
                xAxis: {
                    type: 'category',
                    data: ['02.18', '02.19', '02.20', '02.21', '02.22', '02.23', '02.24', '02.25', '02.26', '02.27', '02.28', '02.29', '02.30', '02.31'],
                    boundaryGap: false,
                    splitLine: {
                        show: true,
                        interval: 'auto',
                        lineStyle: {
                            color: ['#D4DFF5']
                        }
                    },
                    axisTick: {
                        show: false
                    },
                    splitLine: {
                        show: false
                    },
                    axisLine: {
                        show: false
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 14
                        }
                    }
                },
                yAxis: {
                    type: 'value',
                    splitLine: {
                        show: false
                    },
                    axisTick: {
                        show: false
                    },
                    axisLine: {
                        show: false
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 14
                        }
                    }
                },
                series: [{
                    name: '',
                    type: 'line',
                    smooth: true,
                    showSymbol: false,
                    symbol: 'circle',
                    symbolSize: 2,
                    data: ['926', '288', '200', '400', '888', '781', '300', '200', '288', '300', '400', '781', '926', '888'],
                    areaStyle: {
                        normal: {
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                offset: 0,
                                color: '#409EFF'
                            }, {
                                offset: 1,
                                color: '#409EFF'
                            }], false)
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: '#409EFF'
                        }
                    },
                    lineStyle: {
                        normal: {
                            width: 1
                        }
                    }
                }]
            };
            mychart.setOption(option, true);
        },
        alarm_type_t_echarts() {
            var mychart = echarts.init(document.getElementById("alarm_type_t"));
            var option = {
                grid: {
                    left: 5, top: 2, bottom: 8, right: 5,
                },
                xAxis: {
                    type: 'category',
                    data: ['02.18', '02.19', '02.20', '02.21', '02.22', '02.23', '02.24', '02.25', '02.26', '02.27', '02.28', '02.29', '02.30', '02.31'],
                    boundaryGap: false,
                    splitLine: {
                        show: true,
                        interval: 'auto',
                        lineStyle: {
                            color: ['#D4DFF5']
                        }
                    },
                    axisTick: {
                        show: false
                    },
                    splitLine: {
                        show: false
                    },
                    axisLine: {
                        show: false
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 14
                        }
                    }
                },
                yAxis: {
                    type: 'value',
                    splitLine: {
                        show: false
                    },
                    axisTick: {
                        show: false
                    },
                    axisLine: {
                        show: false
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 14
                        }
                    }
                },
                series: [{
                    name: '',
                    type: 'line',
                    smooth: true,
                    showSymbol: false,
                    symbol: 'circle',
                    symbolSize: 2,
                    data: ['200', '926', '300', '288', '300', '400', '200', '400', '888', '888', '781', '926', '288', '300', '781'],
                    areaStyle: {
                        normal: {
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                offset: 0,
                                color: '#729048'
                            }, {
                                offset: 1,
                                color: '#729048'
                            }], false)
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: '#729048'
                        }
                    },
                    lineStyle: {
                        normal: {
                            width: 1
                        }
                    }
                }]
            };
            mychart.setOption(option, true);
        },

        gotoworldmap() {
            this.$router.push({
                path: '/WorldMap'
            })

        },
        // 柱状图
        risk_echarts() {
            var mychart = echarts.init(document.getElementById("risk"));
            var option = {
                tooltip: {
                    trigger: 'axis',
                    axisPointer: {            // 坐标轴指示器，坐标轴触发有效
                        type: 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
                    }
                },
                grid: {
                    left: '10',
                    right: '20',
                    bottom: '10',
                    top: '10',
                    containLabel: true
                },
                xAxis: {
                    type: 'value',
                    axisLine: {
                        lineStyle: {
                            color: '#fff'
                        }
                    },
                    axisTick: {
                        show: false
                    },
                    splitLine: {
                        show: false
                    }
                },
                yAxis: {
                    type: 'category',
                    data: ['192.168.1.193', '192.168.1.193', '192.168.1.193', '192.168.1.193', '192.168.1.193'],
                    axisLine: {
                        lineStyle: {
                            color: '#fff'
                        },

                    },
                    axisTick: {
                        show: false
                    },
                    splitLine: {
                        show: false
                    }
                },
                series: [
                    {
                        name: '高',
                        type: 'bar',
                        stack: '总量',
                        barWidth: 15,
                        label: {
                            normal: {
                                show: true,
                                position: 'insideRight'
                            }
                        },
                        itemStyle: {
                            normal: {
                                barBorderRadius: [4, 0, 0, 4], //柱形图圆角，初始化效果
                                color: 'rgba(150,33,22,.8)',
                            }
                        },
                        data: [301, 334, 390, 330, 320]
                    },
                    {
                        name: '中',
                        type: 'bar',
                        stack: '总量',
                        barWidth: 15,
                        label: {
                            normal: {
                                show: true,
                                position: 'insideRight'
                            }
                        },
                        itemStyle: {
                            normal: {
                                color: 'rgba(245,191,65,.8)',
                            }
                        },
                        data: [101, 134, 90, 230, 210]
                    },
                    {
                        name: '低',
                        type: 'bar',
                        stack: '总量',
                        barWidth: 15,
                        label: {
                            normal: {
                                show: true,
                                position: 'insideRight'
                            }
                        },
                        itemStyle: {
                            normal: {
                                barBorderRadius: [0, 4, 4, 0], //柱形图圆角，初始化效果
                                color: 'rgba(74,164,110,.8)',
                            }
                        },
                        data: [191, 234, 290, 330, 310]
                    },
                ]
            };
            mychart.setOption(option, true);
        },
        tableRowStyle({ row, rowIndex }) {
            return 'background-color:rgba(6, 33, 65, 0.5);color:#fff;'
        },
        tableHeaderColor({ row, column, rowIndex, columnIndex }) {
            return 'background-color:rgba(6, 33, 65, 0.5);color:#78710A;'
        },
        HeaderColor({ row, column, rowIndex, columnIndex }) {
            return 'background-color:rgba(6, 33, 65, 0.5);color:#fff;'
        },
        // 拓扑图
        info_relation_echarts() {
            var mychart = echarts.init(document.getElementById("info_relation"));
            var option = {
                tooltip: {},
                animationDurationUpdate: 1500,
                animationEasingUpdate: 'quinticInOut',
                color: ['#83e0ff', '#45f5ce', '#b158ff'],
                series: [
                    {
                        type: 'graph',
                        layout: 'force',
                        force: {
                            repulsion: 100,
                            edgeLength: 50
                        },
                        symbolSize: 20,
                        roam: true,
                        label: {
                            normal: {
                                show: true
                            }
                        },
                        edgeSymbolSize: [2, 3],
                        edgeLabel: {
                            normal: {
                                show: true,
                                textStyle: {
                                    fontSize: 4,
                                    color: '#fff'
                                },
                                formatter: "{c}"
                            }
                        },
                        data: [
                            {
                                name: 'IP:123.45.67.89',
                                symbolSize: 30,
                                draggable: true,
                                category: 1,
                            },
                            {
                                name: 'URL:WWW.BADDOM.COM',
                                symbolSize: 30,
                                draggable: true, //节点可拖拽
                                category: 1,
                            },
                            {
                                name: 'MAL:A07DVJHKYFG',
                                symbolSize: 20,
                            },
                            {
                                name: 'MAL:A0KYFG',
                                symbolSize: 20,
                            },
                            {
                                name: 'EML:JSKS@126.COM',
                                symbolSize: 20,
                            },
                            {
                                name: 'EML:FSAW@163.COM',
                                symbolSize: 20,
                            },
                            {
                                name: 'IP:48.23.123.178',
                                symbolSize: 20,
                                category: 1,
                            },
                            {
                                name: 'IP:192.168.12.183',
                                symbolSize: 20,
                                category: 1,
                            },
                            {
                                name: 'EML:QQsss@qq.COM',
                                symbolSize: 20,
                                category: 1,
                            },
                            {
                                name: 'IP:192.168.12.163',
                                symbolSize: 20,
                                category: 0,
                            },
                            {
                                name: 'EML:RTUSK@126.COM',
                                symbolSize: 20,
                                category: 0,
                            },
                            {
                                name: 'IP:192.168.1.178',
                                category: 0,
                            },
                        ],
                        itemStyle: {
                            normal: {
                                borderColor: '#FF7000',
                                borderWidth: 2,
                                shadowBlur: 10,
                                color: '#001c43',
                                fontSzie: 8
                            }
                        },
                        links: [
                            {
                                source: 'IP:123.45.67.89',
                                target: 'IP:192.168.12.183',
                                value: '',
                            },

                            {
                                source: 'IP:123.45.67.89',
                                target: 'EML:QQsss@qq.COM',
                                value: '',
                            },
                            // URL:WWW.BADDOM.COM
                            {
                                source: 'URL:WWW.BADDOM.COM',
                                target: 'IP:48.23.123.178',
                                value: '',
                            },
                            {
                                source: 'URL:WWW.BADDOM.COM',
                                target: 'MAL:A0KYFG',
                                value: '',
                            },
                            {
                                source: 'MAL:A0KYFG',
                                target: 'EML:JSKS@126.COM',
                                value: '',
                            },
                            {
                                source: 'IP:48.23.123.178',
                                target: 'EML:FSAW@163.COM',
                                value: '',
                            },
                            {
                                source: 'IP:48.23.123.178',
                                target: 'MAL:A07DVJHKYFG',
                                value: '',
                            },
                            {
                                source: 'IP:123.45.67.89',
                                target: 'IP:192.168.12.163',
                                value: '',
                            },
                            {
                                source: 'IP:123.45.67.89',
                                target: 'EML:RTUSK@126.COM',
                                value: '',
                            },
                            {
                                source: 'IP:123.45.67.89',
                                target: 'IP:192.168.12.163'
                            },
                            {
                                source: 'IP:192.168.12.183',
                                target: 'IP:192.168.1.178',
                                value: '',
                            }

                        ],
                        lineStyle: {
                            normal: {
                                opacity: 0.9,
                                width: 2,
                                color: {
                                    type: 'linear',
                                    x: 0,
                                    y: 0,
                                    x2: 0,
                                    y2: 1,
                                    colorStops: [{
                                        offset: 0, color: '#eda553' // 0% 处的颜色
                                    }, {
                                        offset: 1, color: '#7c785b' // 100% 处的颜色
                                    }],
                                    globalCoord: false // 缺省为 false
                                },
                                curveness: 0
                            }
                        },
                        categories: [
                            { name: '人' },
                            { name: '物证' },
                            { name: '不明物体' }
                        ]
                    },
                ]
            }
            mychart.setOption(option, true);
        },
        // 折线图
        disk_trend_echarts() {
            var mychart = echarts.init(document.getElementById("disk_trend"));
            var option = {
                tooltip: {
                    trigger: 'axis',
                    axisPointer: {
                        lineStyle: {
                            color: '#ddd'
                        }
                    },
                    backgroundColor: 'rgba(255,255,255,1)',
                    padding: [5, 10],
                    textStyle: {
                        color: '#7588E4',
                    },
                    extraCssText: 'box-shadow: 0 0 5px rgba(0,0,0,0.3)'
                },
                // legend: {
                //     right: 20,
                //     orient: 'vertical',
                //     data: ['今日', '昨日']
                // },
                xAxis: {
                    type: 'category',
                    data: ['02.18', '02.19', '02.20', '02.21', '02.22', '02.23', '02.24'],
                    boundaryGap: false,
                    splitLine: {
                        show: true,
                        interval: 'auto',
                        lineStyle: {
                            color: ['#D4DFF5']
                        }
                    },
                    axisTick: {
                        show: false
                    },
                    splitLine: {
                        show: false
                    },
                    axisLine: {
                        lineStyle: {
                            color: '#fff'
                        }
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 14
                        }
                    }
                },
                yAxis: {
                    type: 'value',
                    splitLine: {
                        show: false
                    },
                    axisTick: {
                        show: false
                    },
                    axisLine: {
                        lineStyle: {
                            color: '#fff'
                        }
                    },
                    axisLabel: {
                        margin: 10,
                        textStyle: {
                            fontSize: 14
                        }
                    }
                },
                series: [{
                    name: '',
                    type: 'line',
                    smooth: false,
                    showSymbol: false,
                    symbol: 'circle',
                    symbolSize: 2,
                    data: ['200', '400', '888', '781', '926', '288', '300'],
                    areaStyle: {
                        normal: {
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                offset: 0,
                                color: 'rgba(199, 237, 250,0.5)'
                            }, {
                                offset: 1,
                                color: 'rgba(199, 237, 250,0.2)'
                            }], false)
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: '#f7b851'
                        }
                    },
                    lineStyle: {
                        normal: {
                            width: 1
                        }
                    }
                }]
            };
            mychart.setOption(option, true);
        },
        // 中国地图
        china_eachrts() {
            var myChart = echarts.init(document.getElementById("china_map"));
            var nameColor = " rgb(55, 75, 113)";
            var name_fontFamily = '等线';
            var subname_fontSize = 15;
            var name_fontSize = 18;
            var mapName = 'china';
            var data = [
                { name: "北京", value: 177 },
                { name: "福建", value: 116 },
                { name: "河北", value: 99 },
                { name: "山东", value: 92 },
                { name: "内蒙古", value: 91 },
            ];
            var toolTipData = [
                { name: "北京", type: 'IP', ip: '1.1.1.1', category: '僵尸网络C & C', time: '2019 / 03 / 01' },
                { name: "福建", type: 'URL', ip: 'www.ramulr.com', category: '勒索软件', time: '2019 / 03 / 02' },
                { name: "河北", type: 'URL', ip: 'www.mal.com', category: '恶意地址', time: '2019 / 02 / 28' },
                { name: "山东", type: 'IP', ip: '1.1.1.2', category: '僵尸网络C & C', time: '2019 / 03 / 01' },
                { name: "内蒙古", type: 'URL', ip: 'www.mal.com', category: '恶意地址', time: '2019 / 02 / 11' },
            ];

            var geoCoordMap = {};


            /*获取地图数据*/
            myChart.showLoading();
            var mapFeatures = echarts.getMap(mapName).geoJson.features;
            myChart.hideLoading();
            mapFeatures.forEach(function (v) {
                // 地区名称
                var name = v.properties.name;
                // 地区经纬度
                geoCoordMap[name] = v.properties.cp;

            });
            var max = 480,
                min = 9; // todo 
            var maxSize4Pin = 100,
                minSize4Pin = 20;
            var convertData = function (data) {
                var res = [];
                for (var i = 0; i < data.length; i++) {
                    var geoCoord = geoCoordMap[data[i].name];
                    if (geoCoord) {
                        res.push({
                            name: data[i].name,
                            value: geoCoord.concat(data[i].value),
                        });
                    }
                }
                return res;
            };
            var option = {
                tooltip: {
                    trigger: 'item',
                    formatter: function (params) {
                        console.log(params.name);
                        var toolTiphtml = ''
                        for (var i = 0; i < toolTipData.length; i++) {
                            console.log(toolTipData[i].name);
                            if (params.name == toolTipData[i].name) {
                                console.log(111);

                                toolTiphtml = '<p style="text-align: left;"> ' + toolTipData[i].type + ':' + toolTipData[i].ip + '</p> <p style="text-align:left;"> 威胁:' +
                                    toolTipData[i].category + '</p> <p style="text-align: left;">首次发现时间:' + toolTipData[i].time + '</p>'
                            };
                        }
                        return toolTiphtml;
                    },
                    backgroundColor: 'rgba(0,0,0,0.3)', // 背景
                    padding: [8, 10], //内边距
                    extraCssText: 'box-shadow: 0 0 3px rgba(255, 255, 255, 0.87);', //添加阴影
                    showContent: true,  //是否显示提示框浮层，默认显示
                    alwaysShowContent: true,  // 是否永远显示提示框内容，默认情况下在移出可触发提示框区域后 一定时间 后隐藏，设置为 true 可以保证一直显示提示框内容。
                },
                geo: {
                    show: true,
                    map: mapName,
                    label: {
                        normal: {
                            show: false
                        },
                        emphasis: {
                            show: false,
                        }
                    },
                    roam: false,
                    itemStyle: {
                        normal: {
                            areaColor: "rgba(65,149,210,.6)", //区域颜色　　　　　　　　　
                            borderColor: '#3B5077',
                        },
                        emphasis: {
                            areaColor: '#2B91B7',
                        }
                    }
                },
                series: [{
                    name: '散点',
                    type: 'scatter',
                    coordinateSystem: 'geo',
                    data: convertData(data),
                    symbolSize: '2',
                    label: {
                        normal: {
                            formatter: '{b}',
                            position: 'left',
                            show: true
                        },
                        emphasis: {
                            show: true
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: '#05C3F9'
                        }
                    }
                },
                {
                    type: 'map',
                    map: mapName,
                    geoIndex: 0,
                    aspectScale: 0.75, //长宽比
                    showLegendSymbol: false, // 存在legend时显示
                    label: {
                        normal: {
                            show: true
                        },
                        emphasis: {
                            show: false,
                            textStyle: {
                                color: '#fff'
                            }
                        }
                    },
                    roam: true,
                    itemStyle: {
                        normal: {
                            areaColor: '#031525',
                            borderColor: '#3B5077',
                        },
                        emphasis: {
                            areaColor: '#2B91B7'
                        }
                    },
                    animation: false,
                    data: data
                }, {
                    name: 'Top 5',
                    type: 'effectScatter',
                    coordinateSystem: 'geo',
                    data: toolTipData[1],
                    symbolSize: '5',
                    showEffectOn: 'render',
                    rippleEffect: {
                        brushType: 'stroke'
                    },
                    hoverAnimation: true,
                    label: {
                        normal: {
                            formatter: '{b}',
                            position: 'right',
                            show: true
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: 'yellow',
                            shadowBlur: 10,
                            shadowColor: 'yellow'
                        }
                    },
                    zlevel: 1
                },
                ]
            };

            myChart.setOption(option);
            var dataindex = 0;
            var setindexfun = function () {
                console.log(dataindex);
                myChart.dispatchAction({
                    type: 'showTip',
                    // 系列的 index，在 tooltip 的 trigger 为 axis 的时候可选。
                    seriesIndex: 0,
                    dataIndex: dataindex,
                })
                dataindex++;
                if (dataindex > toolTipData.length - 1) {
                    dataindex = 0;
                }
                // myChart.setOption(option, true);
                setTimeout(setindexfun, 2000);
            }
            setindexfun();
        }

    }
}
</script>
