<template>
  <div class="mod-demo-echarts">
    <el-alert
      title="统计中心"
      type="success"
      :closable="false">
    </el-alert>

    <el-row :gutter="20">
     <el-col :span="12">
        <el-card>
          <div id="J_chartLineBox" class="chart-box"></div>
        </el-card>
      </el-col>
      <el-col :span="12">
        <el-card>
          <div id="J_chartLineBoxMouth" class="chart-box"></div>
        </el-card>
      </el-col>
      <el-col :span="24">
        <el-card>
          <div id="J_chartLineBoxDay" class="chart-box"></div>
        </el-card>
      </el-col>
      <el-col :span="24">
        <el-card>
          <div id="J_chartLineBoxWeek" class="chart-box"></div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import * as echarts from 'echarts';
  export default {
    data () {
      return {
        chartLine: null,
        chartBar: null,
        chartPie: null,
        chartScatter: null,
        option: {
          title: {
            text: '总消费-分类占比',
            subtext: '单位:元',
            left: 'center'
          },
          toolbox: {
            feature: {
              saveAsImage: {}
            }
          },
          tooltip: {
            trigger: 'item'
          },
          legend: {
            orient: 'vertical',
            left: 'left'
          },
          series: [
            {
              name: 'Access From',
              type: 'pie',
              radius: '60%',
              data: [
              ],
              emphasis: {
                itemStyle: {
                  shadowBlur: 10,
                  shadowOffsetX: 0,
                  shadowColor: 'rgba(0, 0, 0, 0.5)'
                }
              },
              label: {
                  normal: {
                      show: true,
                      formatter: '{b}:{c}' + '\n\r' + '({d}%)'
                  }
              }
            }
          ]
        },
        chartLineMouth: null,
        chartBarMouth: null,
        chartPieMouth: null,
        chartScatterMouth: null,
        optionMouth: {
          title: {
            text: '月消费-分类占比',
            subtext: '单位:元',
            left: 'center'
          },
          toolbox: {
            feature: {
              saveAsImage: {}
            }
          },
          tooltip: {
            trigger: 'item'
          },
          legend: {
            orient: 'vertical',
            left: 'left'
          },
          series: [
            {
              name: 'Access From',
              type: 'pie',
              radius: '60%',
              data: [
              ],
              emphasis: {
                itemStyle: {
                  shadowBlur: 10,
                  shadowOffsetX: 0,
                  shadowColor: 'rgba(0, 0, 0, 0.5)'
                }
              },
              label: {
                  normal: {
                      show: true,
                      formatter: '{b}:{c}' + '\n\r' + '({d}%)'
                  }
              }
            }
          ]
        },

        chartLineOut: null,
        chartBarOut: null,
        chartPieOut: null,
        chartScatterOut: null,
        optionOut: {
            title: {
              text: '按天统计-消费(单位:元/天)'
            },
            toolbox: {
              feature: {
                saveAsImage: {}
              }
            },
            xAxis: {
              type: 'category',
              data: []
            },
            yAxis: {
              type: 'value'
              // min: 7300,
              // max: 8000,
            },
            series: [
              {
                data: [],
                type: 'line',
                itemStyle : { normal: {label : {show: true}}}
              }
            ]
        },
        chartLineIn: null,
        chartBarIn: null,
        chartPieIn: null,
        chartScatterIn: null,
        optionIn: {
          title: {
              text: '按周统计-消费(单位:元/周)'
            },
          toolbox: {
            feature: {
              saveAsImage: {}
            }
          },
          xAxis: {
            type: 'category',
            data: []
          },
          yAxis: {
            type: 'value'
          },
          series: [
            {
              data: [],
              type: 'line',
              itemStyle : { normal: {label : {show: true}}}
            }
          ]
        }
      }
    },
    mounted () {
      this.initChartLine();
      this.initChartLineOut();
      this.initChartLineIn();
      this.initChartLineMouth();
    },
    activated () {
      // 由于给echart添加了resize事件, 在组件激活时需要重新resize绘画一次, 否则出现空白bug
      if (this.chartLineOut) {
        this.chartLineOut.resize()
      }
      if (this.chartBarOut) {
        this.chartBarOut.resize()
      }
      if (this.chartPieOut) {
        this.chartPieOut.resize()
      }
      if (this.chartScatterOut) {
        this.chartScatterOut.resize()
      }

      if (this.chartLineIn) {
        this.chartLineIn.resize()
      }
      if (this.chartBarIn) {
        this.chartBarIn.resize()
      }
      if (this.chartPieIn) {
        this.chartPieIn.resize()
      }
      if (this.chartScatterIn) {
        this.chartScatterIn.resize()
      }

      
      if (this.chartLine) {
        this.chartLine.resize()
      }
      if (this.chartBar) {
        this.chartBar.resize()
      }
      if (this.chartPie) {
        this.chartPie.resize()
      }
      if (this.chartScatter) {
        this.chartScatter.resize()
      }

      if (this.chartLineMouth) {
        this.chartLineMouth.resize()
      }
      if (this.chartBarMouth) {
        this.chartBarMouth.resize()
      }
      if (this.chartPieMouth) {
        this.chartPieMouth.resize()
      }
      if (this.chartScatterMouth) {
        this.chartScatterMouth.resize()
      }
    },
    methods: {
      // 按天统计-消费折线图
      initChartLineOut () {
        this.chartLineOut = echarts.init(document.getElementById('J_chartLineBoxDay'))
        //发送请求获取当前节点最新的数据
        this.$http({
          url: this.$http.adornUrl('/booking/record/basicLineChartOut'),
          method: "get",
          params: {"type":"day","inOut": "支出"}
          })
          .then(({ data }) => {
            //请求成功            
            // console.log("要回显的数据name",  data.data.name);
            // console.log("要回显的数据data",  data.data.data);
            for(var i=0;i<data.data.name.length;i++){
                // console.log("要回显的数据name",  data.data.name[i]);
              this.optionOut.xAxis.data.push(data.data.name[i]);
            }
            for(var i=0;i<data.data.data.length;i++){
              // console.log("要回显的数据data",  data.data.data[i]);
              this.optionOut.series[0].data.push(data.data.data[i]);
            }
            this.chartLineOut.setOption(this.optionOut)
          }).catch(() => {});

          // console.log("this.option.xAxis.data", this.option.xAxis.data);
          // console.log("this.option.series[0].data", this.option.series[0].data);
          window.addEventListener('resize', () => {
            this.chartLineOut.resize()
          })
      },

      // 按周统计-消费折线图
      initChartLineIn () {
        this.chartLineIn = echarts.init(document.getElementById('J_chartLineBoxWeek'))        
        this.$http({
          url: this.$http.adornUrl('/booking/record/basicLineChartOut'),
          method: "get",
          params: {"type":"week","inOut": "支出"}
          })
          .then(({ data }) => {
            for(var i=0;i<data.data.name.length;i++){
              this.optionIn.xAxis.data.push(data.data.name[i]);
            }
            for(var i=0;i<data.data.data.length;i++){
              this.optionIn.series[0].data.push(data.data.data[i]);
            }
            this.chartLineIn.setOption(this.optionIn)
          }).catch(() => {});

          window.addEventListener('resize', () => {
            this.chartLineIn.resize()
          })
      },

      // 总消费-饼状图
        initChartLine () {
        this.chartLine = echarts.init(document.getElementById('J_chartLineBox'))        
        this.$http({
        url: this.$http.adornUrl('/booking/record/categoryMoney'),
        method: "get",
        params: {"startTime":"","endTime": ""}
        })
        .then(({ data }) => {
          // for(var i=0;i<data.data.name.length;i++){
          //   this.optionIn.xAxis.data.push(data.data.name[i]);
          // }
          // for(var i=0;i<data.data.data.length;i++){
          //   this.optionIn.series[0].data.push(data.data.data[i]);
          // }
          // console.log("要回显的数据1",  data.data);
          // console.log("要回显的数据2",  this.option.series[0].data);
          this.option.series[0].data=data.data;

          this.chartLine.setOption(this.option)
        }).catch(() => {});

        window.addEventListener('resize', () => {
          this.chartLine.resize()
        })
      },

      //月消费- 饼状图
        initChartLineMouth () {
        this.chartLineMouth = echarts.init(document.getElementById('J_chartLineBoxMouth'))        
        this.$http({
        url: this.$http.adornUrl('/booking/record/categoryMoney'),
        method: "get",
        params: {"startTime":"2022-07-09 00:00:00","endTime": "2022-07-09 23:59:59"}
        })
        .then(({ data }) => {
          // for(var i=0;i<data.data.name.length;i++){
          //   this.optionIn.xAxis.data.push(data.data.name[i]);
          // }
          // for(var i=0;i<data.data.data.length;i++){
          //   this.optionIn.series[0].data.push(data.data.data[i]);
          // }
          // console.log("要回显的数据1",  data.data);
          // console.log("要回显的数据2",  this.option.series[0].data);
          this.optionMouth.series[0].data=data.data;

          this.chartLineMouth.setOption(this.optionMouth)
        }).catch(() => {});

        window.addEventListener('resize', () => {
          this.chartLineMouth.resize()
        })
      }
    }
  }
</script>

<style lang="scss">
  .mod-demo-echarts {
    > .el-alert {
      margin-bottom: 10px;
    }
    > .el-row {
      margin-top: -10px;
      margin-bottom: -10px;
      .el-col {
        padding-top: 10px;
        padding-bottom: 10px;
      }
    }
    .chart-box {
      min-height: 400px;
    }
  }
</style>
