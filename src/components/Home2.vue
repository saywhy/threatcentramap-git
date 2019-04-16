<template>
    <div class="home">

        <span class="icon_full" @click="getFullCreeen">
            <img v-if="full_if" src="../assets/img/full.png" alt="">
            <img v-else src="../assets/img/outfull.png" alt="">
            <span class="full_text">
                {{fun_text}}
            </span>
        </span>

        <div class="main">
            <p class="main_top">白泽威胁情报系统</p>
            <div class="main_bom">
                <div class="main_bom_item">
                    <p class="main_bom_item_text">情报总数</p>
                    <p class="main_bom_item_num">
                        <span v-for=" item in total_intelligence_num" class="main_bom_item_num_span">{{item}}</span>
                    </p>
                </div>
                <div class="main_bom_item">
                    <p class="main_bom_item_text">互联网资产总数</p>
                    <p class="main_bom_item_num">
                        <span v-for=" item in total_net_assets" class="main_bom_item_num_span">{{item}}</span>
                    </p>
                </div>
                <div class="main_bom_item">
                    <p class="main_bom_item_text">风险资产总数</p>
                    <p class="main_bom_item_num">
                        <span v-for=" item in total_risk_attack" class="main_bom_item_num_span">{{item}}</span>
                    </p>
                </div>
                <div class="main_bom_item">
                    <p class="main_bom_item_text">威胁预警总数</p>
                    <p class="main_bom_item_num">
                        <span v-for=" item in total_threat_warning" class="main_bom_item_num_span">{{item}}</span>
                    </p>
                </div>
            </div>
        </div>
        <div class="title">
        </div>
        <!-- 主要内容 -->
        <div class="container">
            <!-- 左边 -->
            <div class="content_left">
                <!-- 左上 -->
                <div class="content_left_top item_common">
                    <img class="border_line_left" src="../assets/img/border_line.png" alt="">
                    <img class="border_line_mid" src="../assets/img/border_line.png" alt="">
                    <img class="border_line_right" src="../assets/img/border_line.png" alt="">
                    <div class="title_top">
                        <img src="../assets/img/title_icon.png" alt="">
                        <span>威胁概览</span>
                    </div>
                    <div class="content_left_top_left">
                        <div id="pie_left"></div>
                    </div>
                    <div class="content_left_top_right">
                        <div id="pie_right"></div>
                    </div>
                </div>
                <!-- 左中 -->
                <div class="content_left_mid item_common">
                    <img class="border_line_left" src="../assets/img/border_line.png" alt="">
                    <img class="border_line_right" src="../assets/img/border_line.png" alt="">
                    <div class="title_top">
                        <img src="../assets/img/title_icon.png" alt="">
                        <span>首要预警</span>
                    </div>
                    <div class="content_left_mid_mid">
                        <div class="alarm_top">
                            <div class="alarm_item alarm_item_name">
                                <span v-text="alarmTypeData.fName"></span>
                            </div>
                            <div class="alarm_item alarm_item_echarts" id="alarm_type_f"></div>
                            <div class="alarm_item alarm_item_num">
                                <span>{{alarmTypeData.fNum}}</span>
                            </div>
                        </div>
                        <div class="alarm_mid">
                            <div class="alarm_item alarm_item_name">
                                <span v-text="alarmTypeData.sName"></span>
                            </div>
                            <div class="alarm_item alarm_item_echarts" id="alarm_type_s"></div>
                            <div class="alarm_item alarm_item_num">
                                <span>{{alarmTypeData.sNum}}</span>
                            </div>
                        </div>
                        <div class="alarm_bom">
                            <div class="alarm_item alarm_item_name">
                                <span v-text="alarmTypeData.tName"></span>
                            </div>
                            <div class="alarm_item alarm_item_echarts" id="alarm_type_t"></div>
                            <div class="alarm_item alarm_item_num">
                                <span>{{alarmTypeData.tNum}}</span>
                            </div>
                        </div>
                    </div>
                    <div class="content_left_mid_bom">
                        <div class="top_bg">
                            <el-row :gutter="0" style="border-bottom:1px solid #6A81B0;">
                                <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6">
                                    <span> </span>
                                </el-col>
                                <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6" :offset="6">
                                    <span>{{alarmTypeData.fName}}</span>
                                </el-col>
                                <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6">
                                    <span>{{alarmTypeData.sName}}</span>
                                </el-col>
                                <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6">
                                    <span>{{alarmTypeData.tName}}</span>
                                </el-col>
                            </el-row>
                        </div>
                        <div class="bom_bg">
                            <el-row :gutter="0">
                                <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6">
                                    <span>{{alarmTypeData.name}} </span>
                                </el-col>
                                <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6">
                                    <span>{{alarmTypeData.fNum}}</span>
                                </el-col>
                                <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6">
                                    <span>{{alarmTypeData.sNum}}</span>
                                </el-col>
                                <el-col :xs="6" :sm="6" :md="6" :lg="6" :xl="6">
                                    <span>{{alarmTypeData.tNum}}</span>
                                </el-col>
                            </el-row>
                        </div>
                    </div>
                </div>
                <!-- 左下 -->
                <div class="content_left_bom item_common">
                    <img class="border_line_left" src="../assets/img/border_line.png" alt="">
                    <img class="border_line_right" src="../assets/img/border_line.png" alt="">
                    <div class="title_top">
                        <img src="../assets/img/title_icon.png" alt="">
                        <span>威胁态势</span>
                        <div class="risk_trend" id="risk_trend">
                        </div>
                    </div>
                </div>
            </div>
            <!-- 中间 -->
            <div class="content_mid">
                <div class="content_mid_map" id="china_map">
                </div>
                <div class="content_mid_bom">
                    <div class="content_mid_bom_top">
                        <el-row :gutter="0">
                            <el-col :xs="8" :sm="8" :md="8" :lg="8" :xl="8">
                                <p>实时情报更新</p>
                            </el-col>
                            <el-col :xs="8" :sm="8" :md="8" :lg="8" :xl="8">
                                <p>实时威胁预警</p>
                            </el-col>
                            <el-col :xs="8" :sm="8" :md="8" :lg="8" :xl="8">
                                <p>预警扩展和关联</p>
                            </el-col>
                        </el-row>
                    </div>
                    <div class="content_mid_bom_bom">
                        <div class="left">
                            <div class="mao_bg">
                                <div class="mao_box">
                                    <span class="left_item" v-for="item in real_time_threat" :class="item.threat?'mao_box_hidden':''">
                                        {{item.name}}
                                    </span>
                                </div>
                                <div class="mao_box_true">
                                    <span class="left_item" v-for="item in real_time_threat" :class="item.threat?'mao_box_red':'mao_box_red_hidden'">
                                        {{item.name}}
                                    </span>
                                </div>
                            </div>
                            <div class="block_left">
                                <div class="block_left_content">
                                    <span class="left_item" v-for="item in real_time_threat">
                                        {{item.name}}
                                    </span>
                                </div>
                            </div>
                        </div>
                        <div class="mid">
                        </div>
                        <div class="right" id="info_relation">

                        </div>
                    </div>
                </div>

            </div>
            <!-- 右边 -->
            <div class="content_right">
                <!-- 右上 -->
                <div class="content_right_top item_common">
                    <img class="border_line_left" src="../assets/img/border_line.png" alt="">
                    <img class="border_line_right" src="../assets/img/border_line.png" alt="">
                    <div class="title_top">
                        <img src="../assets/img/title_icon.png" alt="">
                        <span>全球威胁动态</span>
                    </div>
                    <div class="bom">
                        <div class="bom_item" v-for="item in newsData">
                            <img class="bar_left" src="../assets/img/bar_left.png" alt="">
                            <p class="item_top">
                                <img src="../assets/img/li_title.png" alt="">
                                <span>{{item.name}}</span>
                            </p>
                            <p class="item_bom">
                                <span>{{item.time}}</span>
                            </p>
                        </div>
                    </div>
                </div>
                <!-- 右中 -->
                <div class=" content_right_mid item_common">
                    <img class="border_line_left" src="../assets/img/border_line.png" alt="">
                    <img class="border_line_right" src="../assets/img/border_line.png" alt="">
                    <div class="title_top">
                        <img src="../assets/img/title_icon.png" alt="">
                        <span>威胁分布</span>
                    </div>
                    <div class="threat_content" id="threat">
                    </div>
                </div>
                <!-- 右下 -->
                <div class=" content_right_bom item_common">
                    <img class="border_line_left" src="../assets/img/border_line.png" alt="">
                    <img class="border_line_right" src="../assets/img/border_line.png" alt="">
                    <div class="title_top">
                        <img src="../assets/img/title_icon.png" alt="">
                        <span>威胁排行</span>
                    </div>
                    <div>
                        <el-table :data="tableData" style="width: 100%;" :show-overflow-tooltip="true">
                            <el-table-column prop="ip" label="资产名称" :show-overflow-tooltip="true">
                            </el-table-column>
                            <el-table-column prop="type" label="类型" :show-overflow-tooltip="true">
                            </el-table-column>
                            <el-table-column prop="num" label="威胁数量" :show-overflow-tooltip="true">
                            </el-table-column>
                            <el-table-column prop="src" label="归属" :show-overflow-tooltip="true">
                            </el-table-column>
                        </el-table>
                    </div>
                </div>
            </div>
        </div>

    </div>

</template>
<style  lang="less">
.home {
  height: 1030px;
  width: 1920px;
  position: relative;
  overflow: hidden;
  color: #fff;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  text-align: center;
  background: url(../assets/img/bg4.png) no-repeat 0px 0px;
  background-size: 100% 100%;
  -moz-background-size: 100% 100%;
  padding-top: 50px;
  .icon_full {
    width: 100px;
    height: 37px;
    position: absolute;
    right: 35px;
    top: 7px;
    line-height: 37px;
    background: url(../assets/img/full_bg.png) no-repeat 0px 0px;
    background-size: 100% 100%;
    -moz-background-size: 100% 100%;
    cursor: pointer;
    img {
      vertical-align: middle;
    }
  }
  * {
    box-sizing: border-box;
  }
  div {
    box-sizing: border-box;
  }
  .main {
    width: 720px;
    height: 200px;
    position: absolute;
    left: 50%;
    top: 0;
    transform: translateX(-50%);
    z-index: 99999;
    background: url(../assets/img/title_text_bg.png) no-repeat 0px 0px;
    background-size: 100% 100%;
    -moz-background-size: 100% 100%;
    .main_top {
      font-weight: 700;
      height: 50px;
      margin-top: 28px;
      font-size: 35px;
      font-family: PingFangSC-Regular, sans-serif;
      background-image: -webkit-gradient(
        linear,
        0 0,
        0 bottom,
        from(#54ffff),
        to(#3c8eff)
      );
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
    .main_bom {
      position: absolute;
      //   border: 1px solid red;
      bottom: 0;
      height: 70px;
      width: 100%;
      .main_bom_item {
        float: left;
        width: 25%;
        height: 70px;
        // padding: 0px 10px;
        // border: 1px solid red;
        text-align: center;
        padding-bottom: 30px;
        .main_bom_item_text {
          font-size: 14px;
          color: #fff;
          margin-bottom: 10px;
        }
        .main_bom_item_num {
          .main_bom_item_num_span {
            display: inline-block;
            min-width: 20px;
            margin-right: 5px;
            text-align: center;
            font-family: LcdD;
            font-size: 30px;
            color: #ffffff;
            line-height: 32px;
            background: url(../assets/img/number.png) no-repeat 0px 0px;
            background-size: 100% 100%;
            -moz-background-size: 100% 100%;
          }
        }
      }
    }
  }
  .title {
    height: 46px;
    width: 100%;
    background: url(../assets/img/title_bg.png) no-repeat 0px 0px;
    background-size: 100% 100%;
    -moz-background-size: 100% 100%;
  }
  //   公共部分
  .item_common {
    background: url(../assets/img/item_bg_s.png) no-repeat 0px 0px;
    background-size: 100% 100%;
    -moz-background-size: 100% 100%;
    padding: 0 24px;
    width: 500px;
    height: 300px;
    position: relative;
    .border_line_left {
      height: 260px;
      width: 20px;
      position: absolute;
      left: -10px;
      top: 50%;
      transform: translateY(-50%);
    }
    .border_line_mid {
      position: absolute;
      height: 260px;
      width: 20px;
      left: 50%;
      margin-left: -10px;
      top: 50%;
      transform: translateX(-50%);
      transform: translateY(-50%);
    }
    .border_line_right {
      width: 20px;
      height: 260px;
      position: absolute;
      right: -10px;
      top: 50%;
      transform: translateY(-50%);
    }
    .title_top {
      height: 64px;
      //   border: 1px solid red;
      text-align: left;
      font-size: 16px;
      color: #ffffff;
      line-height: 64px;
      img {
        width: 28px;
        height: 14px;
        margin-right: 5px;
      }
    }
  }
  .container {
    padding: 0 40px;
    //   左边
    .content_left {
      width: 500px;
      height: 944px;
      // border: 1px solid red;
      float: left;
      // 左上
      .content_left_top {
        .content_left_top_left {
          float: left;
          height: 236px;
          width: 50%;
          #pie_left {
            height: 236px;
            width: 100%;
          }
        }
        .content_left_top_right {
          height: 236px;
          width: 50%;
          float: left;
          #pie_right {
            height: 236px;
            width: 100%;
          }
        }
      }
      // 左中
      .content_left_mid {
        margin: 20px 0;
        position: relative;
        .content_left_mid_mid {
          height: 160px;
          padding: 5px 0;
          .alarm_item {
            float: left;
            height: 40px;
            line-height: 44px;
            span {
              font-size: 14px;
            }
          }
          .alarm_item_name {
            width: 70px;
          }
          .alarm_item_echarts {
            width: 320px;
            background: url(../assets/img/alarm_bg.png) no-repeat 0px 0px;
            background-size: 100% 100%;
            -moz-background-size: 100% 100%;
          }
          .alarm_item_num {
            width: 55px;
          }
          .alarm_top {
            height: 50px;
            padding: 2px 0;
          }
          .alarm_mid {
            height: 50px;
            padding: 2px 0;
          }
          .alarm_bom {
            height: 50px;
            padding: 2px 0;
          }
        }
        .content_left_mid_bom {
          height: 74px;
          width: 500px;
          position: absolute;
          bottom: 0;
          left: 0;
          .top_bg {
            height: 37px;
            line-height: 37px;
            background: #275097;
          }
          .bom_bg {
            height: 37px;
            line-height: 37px;
            background: url(../assets/img/bom_bg.png) no-repeat 0px 0px;
            background-size: 100% 100%;
            -moz-background-size: 100% 100%;
          }
        }
      }
      // 左下
      .content_left_bom {
        .risk_trend {
          height: 236px;
          width: 100%;
        }
      }
    }
    // 中间
    .content_mid {
      height: 944px;
      width: 800px;
      margin: 0 20px;
      float: left;
      //   .content_mid_map {
      //     height: 460px;
      //     width: 100%;
      //     margin-top: 138px;
      //     // border: 1px solid red;
      //     margin-bottom: 45px;
      //   }
      .content_mid_map {
        height: 460px;
        width: 100%;
        margin-top: 138px;
        // border: 1px solid red;
        margin-bottom: 45px;
      }
      .content_mid_bom {
        background: url(../assets/img/mid_bom_bg.png) no-repeat 0px 0px;
        background-size: 100% 100%;
        -moz-background-size: 100% 100%;
        height: 300px;
        width: 100%;
        .content_mid_bom_top {
          background: url(../assets/img/mid_bom_top_bg.png) no-repeat 0px 0px;
          background-size: 100% 100%;
          -moz-background-size: 100% 100%;
          height: 42px;
          line-height: 42px;
          font-size: 16px;
        }
        .content_mid_bom_bom {
          height: 270px;
          padding: 10px;
          .left {
            float: left;
            width: 500px;
            height: 100%;
            overflow: hidden;
            text-align: left;
            position: relative;
            font-family: PingFangSC-Regular;
            font-size: 12px;
            color: #ffffff;
            .mao_bg {
              font-family: PingFangSC-Regular;
              font-size: 12px;
              color: #ffffff;
              width: 50%;
              height: 100%;
              position: absolute;
              right: 0;
              top: 0;
              background: url(../assets/img/mao_bg.png) no-repeat 0px 0px;
              background-size: 100% 100%;
              -moz-background-size: 100% 100%;
              overflow: hidden;
              .mao_box {
                filter: blur(2px);
                width: 500px;
                height: 100%;
                overflow: hidden;
                position: absolute;
                left: -250px;
                .mao_box_hidden {
                  opacity: 0;
                }
                .left_item {
                  display: inline-block;
                  padding: 0 10px;
                  background: rgba(255, 255, 255, 0.12);
                  border-radius: 4px;
                  margin-right: 5px;
                  margin-bottom: 10px;
                }
              }
              .mao_box_true {
                width: 500px;
                height: 100%;
                overflow: hidden;
                position: absolute;
                left: -250px;
                .mao_box_red {
                  opacity: 0.8;
                  color: #c3112b;
                  background: rgba(195, 17, 43, 0.24);
                  //   border: 1px solid #c3112b;
                }
                .mao_box_red_hidden {
                  opacity: 0;
                }
                .left_item {
                  //   opacity: 0;
                  display: inline-block;
                  padding: 0 10px;
                  //   background: rgba(255, 255, 255, 0.12);
                  border-radius: 4px;
                  margin-right: 5px;
                  margin-bottom: 10px;
                }
              }
            }
            .block_left {
              width: 250px;
              overflow: hidden;
              .block_left_content {
                width: 500px;
                .left_item {
                  display: inline-block;
                  padding: 0 10px;
                  background: rgba(255, 255, 255, 0.12);
                  border-radius: 4px;
                  margin-right: 5px;
                  margin-bottom: 10px;
                }
              }
            }

            .anim {
              transition: all 0.5s;
            }
          }
          .mid {
            background: url(../assets/img/arrow.png) no-repeat 0px 0px;
            background-size: 100% 100%;
            -moz-background-size: 100% 100%;
            float: left;
            width: 42px;
            height: 200px;
            margin-left: 10px;
            margin-top: 17px;
            // border: 1px solid red;
          }
          .right {
            float: right;
            width: 216px;
            height: 100%;
            // border: 1px solid red;
          }
        }
      }
    }
    // 右边
    .content_right {
      height: 944px;
      width: 500px;
      float: left;
      // 右上
      .content_right_top {
        .bom {
          .bom_item {
            background-color: #00357f;
            border-radius: 4px;
            height: 52px;
            margin: 2px 0;
            padding: 10px 0;
            position: relative;
            p {
              text-align: left;
            }
            .bar_left {
              position: absolute;
              left: 0;
              top: 0;
            }
            .item_top {
              font-size: 14px;
              img {
                margin: 0 10px;
              }
            }
            .item_bom {
              padding-left: 36px;
              opacity: 0.64;
              font-size: 12px;
            }
          }
        }
      }
      // 右中
      .content_right_mid {
        margin: 20px 0;
        .threat_content {
          height: 235px;
        }
      }
      // 右下
      .content_right_bom {
        .el-table {
          color: #fff;
          background-color: rgba(6, 33, 65, 0) !important;
          border-radius: 3px;
        }
        .el-table th {
          color: #2684ff;
        }
        .el-table th,
        .el-table tr {
          background-color: rgba(6, 33, 65, 0);
          font-size: 14px;
        }
        .el-table--enable-row-hover .el-table__body tr:hover > td {
          background-color: rgba(34, 72, 137, 0.56) !important;
          cursor: pointer;
        }
        .el-table td,
        .el-table th.is-leaf {
          border-bottom: 1px solid rgba(151, 151, 151, 0.36);
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
    }
  }
}
</style>

<script>
var echarts = require('echarts');
import 'echarts/map/js/china.js';
import '../../static/china.js';
import '../../static/echarts-auto-tooltip.js';
export default {
    name: 'home',
    data() {
        return {
            // 情报总数
            total_intelligence_num: [0],
            total_net_assets: [0],
            total_risk_attack: [0],
            total_threat_warning: [0],
            alarmTypeData: {
                name: '影响资产数',
                fName: '数据泄露',
                sName: '勒索软件',
                tName: '高危漏洞',
                fNum: 123,
                sNum: 2332,
                tNum: 12213,
            },
            newsData: [
                {
                    name: '所有英特尔处理器面临新的Spoiler攻击',
                    time: '7小时前'
                },
                {
                    name: '微软安全报告显示去年网络钓鱼攻击有所增加',
                    time: '7小时前'
                },
                {
                    name: 'RSA2019|Axonius 获创新沙盒冠军',
                    time: '7小时前'
                },
                {
                    name: 'ji32k7 发现是一个令人震惊的糟糕密码',
                    time: '7小时前'
                },
            ],
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
            }
            ],
            n: 0,
            fun_text: '全屏',
            full_if: true,
            real_time_threat: [
                { name: 'IP:123.45.67.89', threat: false },
                { name: 'MAL:A07DA897FDE02', threat: false },
                { name: 'IP:192.45.1.199', threat: false },
                { name: 'URL:www.baddomm.com', threat: false },
                { name: 'IP:36.15.32.79', threat: true },
                { name: 'MAL:H7HK86HHJF', threat: false },
                { name: 'IP:136.23.173.178', threat: false },
                { name: 'URL:www.swf.com', threat: true },
                { name: 'MAL:K75HJKG986HJG', threat: false },
                { name: 'URL:www.baiduyunpan.com', threat: false },
                { name: 'IP:36.15.32.79', threat: false },
                { name: 'MAL:F78HGH9OTF973', threat: false },
                { name: 'URL:www.baddomm.com', threat: false },
                { name: 'IP:36.15.32.79', threat: true },
                { name: 'MAL:H7HK86HHJF', threat: false },
                { name: 'IP:136.23.173.178', threat: false },
                { name: 'URL:www.swf.com', threat: true },
                { name: 'MAL:K75HJKG986HJG', threat: false },
                { name: 'MAL:H7HK86HHJF', threat: false },
                { name: 'IP:136.23.173.178', threat: false },
            ]
        }
    },
    props: {
        autoPlay: {
            type: Boolean,
            default: true
        },
        interval: {
            type: Number,
            default: 9000
        },
    },
    mounted() {
        // 左上
        this.pie_left_echarts();
        this.pie_right_echarts();
        // 左中
        this.alarm_type_f_echarts();
        this.alarm_type_s_echarts();
        this.alarm_type_t_echarts();
        // 左下
        this.risk_trend_echarts();
        // 中上
        setInterval(() => {
            this.china_eachrts();
        }, 2000)
        this.echarts_map();
        // 中下
        this.info_relation_echarts();
        // 右上
        // 右中-柱状图
        this.threat_echarts();
        // 右下
        this.get_data();
        this.real_time_data();
        this.realtime_alert();
        this.total_risk_attack_get();
        this.total_intelligence_num_get();

    },
    methods: {
        numHandle(params) {
            if (params <= 999) {
                params = params.toString(); // 
            } else if (999 < params && params <= 99999) {
                params = params / 1000;
                params = params.toString().split(".")[0] + '.' + params.toString().split(".")[1].substr(0, 1) + 'K'; // k 千
            } else if (99999 < params && params <= 9999999) {
                params = params / 100000;
                params = params.toString().split(".")[0] + '.' + params.toString().split(".")[1].substr(0, 1) + 'M'; // m 兆
            } else if (9999999 < params && params <= 999999999) {
                params = params / 10000000;
                params = params.toString().split(".")[0] + '.' + params.toString().split(".")[1].substr(0, 1) + 'G'; // g 吉（咖）
            } else if (999999999 < params && params <= 99999999999) {
                params = params / 1000000000;
                params = params.toString().split(".")[0] + '.' + params.toString().split(".")[1].substr(0, 1) + 'T'; //t 太（拉）
            } else if (params > 99999999999 && params <= 99999999999999) {
                params = params / 100000000000;
                params = params.toString().split(".")[0] + '.' + params.toString().split(".")[1].substr(0, 1) + 'P'; //p 拍（它）
            } else if (params > 99999999999 && params <= 99999999999999) {
                params = params / 100000000000000;
                params = params.toString().split(".")[0] + '.' + params.toString().split(".")[1].substr(0, 1) + 'E'; //e 艾
            } else if (params > 99999999999999 && params <= 99999999999999999) {
                params = params / 100000000000000000;
                params = params.toString().split(".")[0] + '.' + params.toString().split(".")[1].substr(0, 1) + 'Z'; //z 泽
            }
            return params;
        },
        converStr(str) {
            if (/\./.test(str)) {
                return str.replace(/\d(?=(\d{1})+\.)/g, "$&,").split("").reverse().join("").replace(/\d(?=(\d{1})+\.)/g, "$&,").split("").reverse().join("");
            } else {
                return str.replace(/\d(?=(\d{1})+$)/g, "$&,");
            }
        },
        // 风险资产总数
        total_risk_attack_get() {
            this.$axios.get('/demonstration/risk-assets-count')
                .then(response => {
                    var str = this.numHandle(response.data.data.risk_assets_count);
                    this.total_risk_attack = str.split("");
                })
                .catch(error => {
                    console.log(error);
                })
        },

        // 情报总数
        total_intelligence_num_get() {
            this.$axios.get('/demonstration/intelligence-count ')
                .then(response => {
                    var str = this.numHandle(response.data.data.total_intelligence);
                    this.total_intelligence_num = str.split("");
                })
                .catch(error => {
                    console.log(error);
                })
        },
        real_time_data() {
            setInterval(() => {
                var item = this.real_time_threat.shift();
                this.real_time_threat.push(item);
            }, 2000)
        },
        // 左上-威胁分布-饼图
        pie_left_echarts() {
            this.$axios.get('/demonstration/threat-level-distribution')
                .then(response => {
                    var pie_left_echarts_data = [
                        { name: '高', value: 0 },
                        { name: '中', value: 0 },
                        { name: '低', value: 0 }
                    ];
                    response.data.data.forEach(item => {
                        if (item.degree == '高') {
                            pie_left_echarts_data[0].name = item.degree
                            pie_left_echarts_data[0].value = item.count
                        }
                        if (item.degree == '中') {
                            pie_left_echarts_data[1].name = item.degree
                            pie_left_echarts_data[1].value = item.count
                        }
                        if (item.degree == '低') {
                            pie_left_echarts_data[2].name = item.degree
                            pie_left_echarts_data[2].value = item.count
                        }

                    })
                    var mychart = echarts.init(document.getElementById("pie_left"));
                    var option = {
                        title: {
                            text: '威胁等级分布',
                            left: 'center',
                            top: 10,
                            textStyle: {
                                fontSize: 14,
                                color: '#fff'
                            }
                        },
                        tooltip: {
                            show: true
                        },
                        legend: {
                            orient: 'horizontal',
                            bottom: 22,
                            left: 'center',
                            textStyle: {
                                color: '#fff',
                                fontSize: 12
                            },
                            icon: 'circle',
                            itemWidth: 6,  // 设置宽度
                            itemHeight: 6, // 设置高度
                            data: ['高', '中', '低']
                        },
                        color: ['#FF5F5C', '#FEAA00', '#12DCFF'],
                        series: [
                            {
                                name: '',
                                type: 'pie',
                                radius: ['35%', '50%'],
                                center: ['50%', '50%'],
                                avoidLabelOverlap: false, //是否启用防止标签重叠策略，默认开启，
                                hoverAnimation: true,//是否开启 hover 在扇区上的放大动画效果。
                                legendHoverLink: true,//是否启用图例 hover 时的联动高亮。
                                selectedOffset: 5,
                                hoverOffset: 2, //高亮扇区的偏移距离。
                                label: {
                                    normal: {
                                        show: false,
                                        position: 'center'
                                    },
                                    emphasis: {
                                        show: true,
                                        formatter: '{d}%\n\n{b}',
                                        textStyle: {
                                            fontSize: '14',
                                            color: '#fff',
                                            fontWeight: 'bold'
                                        }
                                    }
                                },
                                labelLine: {
                                    normal: {
                                        show: false
                                    }
                                },
                                data: pie_left_echarts_data
                            }
                        ]
                    };
                    mychart.setOption(option, true);
                    tools.loopShowTooltip(mychart, option, { loopSeries: true }); // 使用本插件
                })
                .catch(error => {
                    console.log(error);
                })

        },
        pie_right_echarts() {
            this.$axios.get('/demonstration/threat-category')
                .then(response => {
                    console.log(response.data.data);
                    var legend_data = [];
                    var series_data = [];
                    response.data.data.forEach(item => {
                        var obj = {};
                        legend_data.push(item.category);
                        obj.name = item.category;
                        obj.value = item.count;
                        series_data.push(obj);
                    })
                    var mychart = echarts.init(document.getElementById("pie_right"));
                    var option = {
                        title: {
                            text: '威胁类型分布',
                            left: 'center',
                            top: 10,
                            textStyle: {
                                fontSize: 14,
                                color: '#fff'
                            }
                        },
                        tooltip: {
                            show: true
                        },
                        legend: {
                            orient: 'horizontal',
                            bottom: 0,
                            left: 'center',
                            textStyle: {
                                color: '#fff',
                                fontSize: 12
                            },
                            icon: 'circle',
                            itemWidth: 6,  // 设置宽度
                            itemHeight: 6, // 设置高度
                            data: legend_data
                        },
                        color: ['#0E79FF ', '#9C00E5', '#8DF97F', '#FF35C1'],
                        series: [
                            {
                                name: '',
                                type: 'pie',
                                radius: ['35%', '50%'],
                                center: ['50%', '50%'],
                                avoidLabelOverlap: false, //是否启用防止标签重叠策略，默认开启，
                                hoverAnimation: true,//是否开启 hover 在扇区上的放大动画效果。
                                legendHoverLink: true,//是否启用图例 hover 时的联动高亮。
                                selectedOffset: 5,
                                hoverOffset: 2, //高亮扇区的偏移距离。
                                label: {
                                    normal: {
                                        show: false,
                                        position: 'center'
                                    },
                                    emphasis: {
                                        show: true,
                                        formatter: '{d}%\n\n{b}',
                                        textStyle: {
                                            fontSize: '14',
                                            color: '#fff',
                                            fontWeight: 'bold'
                                        }
                                    }
                                },
                                labelLine: {
                                    normal: {
                                        show: false
                                    }
                                },
                                data: series_data
                            }
                        ]
                    };
                    mychart.setOption(option, true);
                    tools.loopShowTooltip(mychart, option, { loopSeries: true }); // 使用本插件
                })
                .catch(error => {
                    console.log(error);
                })

        },
        // 左中
        alarm_type_f_echarts() {
            var mychart = echarts.init(document.getElementById("alarm_type_f"));
            var option = {
                grid: {
                    left: 0, top: 2, bottom: 0, right: 0,
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
                                color: '#4292FF'
                            }, {
                                offset: 1,
                                color: 'rgba(66,146,255,0.48)'
                            }], false)
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: '#4292FF'
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
                    left: 0, top: 2, bottom: 0, right: 0,
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
                                color: 'rgba(255,107,74,1)'
                            }, {
                                offset: 1,
                                color: 'rgba(255,107,74,0.48)'
                            }], false)
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: 'rgba(255,107,74,1)'
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
                    left: 0, top: 2, bottom: 0, right: 0,
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
                                color: 'rgba(255,167,43,1)'
                            }, {
                                offset: 1,
                                color: 'rgba(255,167,43,0.48)'
                            }], false)
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: 'rgba(255,167,43,1)'
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
        // 左下
        // 折线图
        risk_trend_echarts() {
            this.$axios.get('/demonstration/threat-situation')
                .then(response => {
                    console.log(response.data.data);
                    var xAxis_data = []
                    var series_data = []
                    response.data.data.forEach(item => {
                        xAxis_data.push(item.statistics_time);
                        series_data.push(item.count);
                    })
                    var mychart = echarts.init(document.getElementById("risk_trend"));
                    var option = {
                        tooltip: {
                            trigger: 'axis',
                            axisPointer: {
                                lineStyle: {
                                    image: '', // 支持为 HTMLImageElement, HTMLCanvasElement，不支持路径字符串
                                    repeat: 'repeat' // 是否平铺, 可以是 'repeat-x', 'repeat-y', 'no-repeat'
                                },
                            },
                            backgroundColor: 'rgba(255,255,255,1)',
                            padding: [5, 10],
                            textStyle: {
                                color: '#7588E4',
                            },
                            extraCssText: 'box-shadow: 0 0 5px rgba(0,0,0,0.3)'
                        },
                        xAxis: {
                            type: 'category',
                            data: xAxis_data,
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
                                    color: 'rgba(84,255,255,.36)'
                                }
                            },
                            axisLabel: {
                                color: '#fff',
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
                                    color: 'rgba(84,255,255,.36)'
                                }
                            },
                            axisLabel: {
                                color: '#fff',
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
                            data: series_data,
                            areaStyle: {
                                normal: {
                                    color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                        offset: 0,
                                        color: 'rgba(195,17,43,0.3)'
                                    }, {
                                        offset: 1,
                                        color: 'rgba(195,17,43,0.1)'
                                    }], false)
                                }
                            },
                            itemStyle: {
                                normal: {
                                    color: '#C3112B'
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
                })
                .catch(error => {
                    console.log(error);
                })

        },
        // 中上
        echarts_map() {
            this.$axios.get('https://raw.githubusercontent.com/WingsleyLui/MapJSON/master/global_map2.json')
                .then(response => {
                    var mychart = echarts.init(document.getElementById("content_mid_map"));
                    echarts.registerMap('globalmap', response.data);
                    mychart.setOption({
                        tooltip: {
                            trigger: 'item',
                            formatter: function (item) {
                                // console.log(item);
                            },
                            textStyle: {
                                fontSize: 18
                            }
                        },
                        grid: {
                            left: 0,
                            top: 0,
                            right: 0,
                            bottom: 0
                        },
                        series: [
                            {
                                name: 'Total amount of patients',
                                type: 'map',
                                mapType: 'globalmap',
                                roam: false,
                                zoom: 1.2,
                                label: {
                                    normal: {
                                        show: false
                                    },
                                    emphasis: {
                                        show: true
                                    }
                                },
                                itemStyle: {
                                    normal: {
                                        label: {
                                            show: true
                                        },
                                        borderWidth: .5, //区域边框宽度
                                        borderColor: '#0A68E9', //区域边框颜色
                                        areaColor: "#081F3D", //区域颜色
                                    },
                                    emphasis: {
                                        label: {
                                            show: true
                                        }
                                    }
                                },
                                data: [

                                ],
                                nameMap: {
                                }
                            },
                        ],
                    });
                })
                .catch(error => {
                    console.log(error);
                })
        },
        // 中国地图
        china_eachrts() {
            this.$axios.get('/demonstration/map-alert')
                .then(response => {
                    console.log(response.data.data);
                    if (response.data.data.length == 0) {
                        var toolTipData = [
                        ];
                    } else {
                        var toolTipData = [
                            { name: "上海", type: 'IP', ip: response.data.data.device_ip, category: response.data.data.category, time: '2019/03/01' },
                        ]
                    }
                    var myChart = echarts.init(document.getElementById("china_map"));
                    var nameColor = " rgb(55, 75, 113)";
                    var name_fontFamily = '等线';
                    var subname_fontSize = 15;
                    var name_fontSize = 18;
                    var mapName = 'china';
                    var data = [
                        { name: "上海", value: 177 },
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
                                // console.log(params.name);
                                var toolTiphtml = ''
                                for (var i = 0; i < toolTipData.length; i++) {
                                    // console.log(toolTipData[i].name);
                                    if (params.name == toolTipData[i].name) {
                                        toolTiphtml = '<p style="text-align: left;"> ' + toolTipData[i].type + ':' + toolTipData[i].ip + '</p> <p style="text-align:left;"> 威胁:' +
                                            toolTipData[i].category + '</p> <p style="text-align: left;">首次发现时间:' + toolTipData[i].time + '</p>'
                                    };
                                }
                                return toolTiphtml;
                            },
                            fontFamily: 'PingFangSC-Regular',
                            fontSize: 12,
                            backgroundColor: 'rgba(12,54,188,.62)', // 背景
                            padding: [8, 10], //内边距
                            // extraCssText: 'box-shadow: 0 0 3px rgba(255, 255, 255, 0.87);', //添加阴影
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
                                    // areaColor: "rgba(65,149,210,.6)", //区域颜色　　　　　　　　　
                                    // borderColor: '#3B5077',
                                    borderWidth: .5, //区域边框宽度
                                    borderColor: '#0A68E9', //区域边框颜色
                                    areaColor: "#081F3D", //区域颜色
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
                        // console.log(dataindex);
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
                        // setTimeout(setindexfun, 1000);
                    }
                    setindexfun();
                })
                .catch(error => {
                    console.log(error);
                })

            // tools.loopShowTooltip(myChart, option, { loopSeries: true }); // 使用本插件
        },
        // 中下
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
                        // focusNodeAdjacency: true,
                        force: {
                            repulsion: 100,
                            edgeLength: 50
                        },
                        symbolSize: 20,
                        roam: true,
                        label: {
                            normal: {
                                show: true,//显示
                                color: '#fff',
                                position: 'right',//相对于节点标签的位置，默认在节点中间
                            }
                        },
                        edgeSymbol: ['circle'],//边两端的标记类型
                        // edgeSymbolSize: [4, 8],//边两端的标记大小
                        edgeSymbolSize: [2, 3],
                        edgeLabel: {
                            normal: {
                                show: true,
                                textStyle: {
                                    fontSize: 8,
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
                                itemStyle: {
                                    normal: {
                                        borderColor: '#FF7327',
                                        borderWidth: 2,
                                        shadowBlur: 10,
                                        color: '#FF7327',
                                    }
                                },
                            },
                            {
                                name: 'URL:WWW.BADDOM.COM',
                                symbolSize: 30,
                                draggable: true, //节点可拖拽
                                category: 1,
                                itemStyle: {
                                    normal: {
                                        borderColor: '#FF7327',
                                        borderWidth: 2,
                                        shadowBlur: 10,
                                        color: '#FF7327',
                                    }
                                },
                            },

                            {
                                name: 'MAL:A0KYFG',
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
                        ],
                        itemStyle: {
                            normal: {
                                borderColor: '#DBA500',
                                borderWidth: 2,
                                shadowBlur: 10,
                                color: '#DBA500',
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

                        ],
                        lineStyle: {
                            normal: {
                                opacity: 0.31,
                                width: 1,
                                color: '#fff',
                                curveness: 0.7
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
        // 右上
        // 右中
        threat_echarts() {
            var mychart = echarts.init(document.getElementById("threat"));
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
                    show: false,
                    axisLine: {
                        show: false,
                        lineStyle: {
                            show: false,
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
                    data: ['一分公司', '二分公司', '三分公司', '四分公司', '五分公司'],
                    axisLine: {
                        show: false,
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
                        barWidth: 10,
                        label: {
                            normal: {
                                show: true,
                                position: 'insideRight'
                            }
                        },
                        itemStyle: {
                            normal: {
                                barBorderRadius: [4, 0, 0, 4], //柱形图圆角，初始化效果
                                color: '#FF5F5C',
                            }
                        },
                        data: [301, 334, 390, 330, 320]
                    },
                    {
                        name: '中',
                        type: 'bar',
                        stack: '总量',
                        barWidth: 10,
                        label: {
                            normal: {
                                show: true,
                                position: 'insideRight'
                            }
                        },
                        itemStyle: {
                            normal: {
                                color: '#FEAA00',
                            }
                        },
                        data: [101, 134, 90, 230, 210]
                    },
                    {
                        name: '低',
                        type: 'bar',
                        stack: '总量',
                        barWidth: 10,
                        label: {
                            normal: {
                                show: true,
                                position: 'insideRight'
                            }
                        },
                        itemStyle: {
                            normal: {
                                barBorderRadius: [0, 4, 4, 0], //柱形图圆角，初始化效果
                                color: '#12DCFF',
                            }
                        },
                        data: [191, 234, 290, 330, 310]
                    },
                ]
            };
            mychart.setOption(option, true);
        },
        // 右下
        getFullCreeen() {
            this.n++;
            console.log(this.n);
            this.n % 2 == 0 ? this.outFullCreeen(document) : this.inFullCreeen(document.documentElement);
            this.n % 2 == 0 ? this.fun_text = '全屏' : this.fun_text = '退出';
            this.n % 2 == 0 ? this.full_if = true : this.full_if = false;
        },
        inFullCreeen(element) {
            let el = element;
            let rfs = el.requestFullScreen || el.webkitRequestFullScreen ||
                el.mozRequestFullScreen || el.msRequestFullScreen;
            if (typeof rfs != "undefined" && rfs) {
                rfs.call(el);
            } else if (typeof window.ActiveXObject != "undefined") {
                let wscript = new ActiveXObject("WScript.Shell");
                if (wscript != null) {
                    wscript.SendKeys("{F11}");
                }
            }
        },
        outFullCreeen(element) {
            let el = element;
            let cfs = el.cancelFullScreen || el.webkitCancelFullScreen ||
                el.mozCancelFullScreen || el.exitFullScreen;
            if (typeof cfs != "undefined" && cfs) {
                cfs.call(el);
            } else if (typeof window.ActiveXObject != "undefined") {
                let wscript = new ActiveXObject("WScript.Shell");
                if (wscript != null) {
                    wscript.SendKeys("{F11}");
                }
            }
        },
        // 数据请求
        get_data() {
            this.$axios.get('/email/get')
                .then(response => {
                    console.log(response);
                })
                .catch(error => {
                    console.log(error);
                })

        },
        realtime_alert() {
            this.$axios.get('/demonstration/realtime-alert')
                .then(response => {
                    // console.log(response.data.data);

                })
                .catch(error => {
                    console.log(error);
                })
        }
    }
}
</script>



