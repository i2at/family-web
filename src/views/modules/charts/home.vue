<template>
  <div class="mod-demo-echarts">
    <el-alert
      title="月收入折线图"
      type="success"
      :closable="false">
    </el-alert>

    <el-row :gutter="20">
    <el-col :span="24">
        <el-card>
          <div id="J_chartLineBox" class="chart-box"></div>
        </el-card>
      </el-col>
      <el-col :span="24">
        <el-card>
          <div id="J_chartLineBoxOut" class="chart-box"></div>
        </el-card>
      </el-col>
      <el-col :span="24">
        <el-card>
          <div id="J_chartLineBoxIn" class="chart-box"></div>
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
            text: 'Stacked Line'
          },
          tooltip: {
            trigger: 'axis'
          },
          legend: {
            data: ['Email', 'Union Ads', 'Video Ads', 'Direct', 'Search Engine']
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          toolbox: {
            feature: {
              saveAsImage: {}
            }
          },
          xAxis: {
            type: 'category',
            boundaryGap: false,
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
          },
          yAxis: {
            type: 'value'
          },
          series: [
            {
              name: 'Email',
              type: 'line',
              stack: 'Total',
              data: [120, 132, 101, 134, 90, 230, 210]
            },
            {
              name: 'Union Ads',
              type: 'line',
              stack: 'Total',
              data: [220, 182, 191, 234, 290, 330, 310]
            },
            {
              name: 'Video Ads',
              type: 'line',
              stack: 'Total',
              data: [150, 232, 201, 154, 190, 330, 410]
            },
            {
              name: 'Direct',
              type: 'line',
              stack: 'Total',
              data: [320, 332, 301, 334, 390, 330, 320]
            },
            {
              name: 'Search Engine',
              type: 'line',
              stack: 'Total',
              data: [820, 932, 901, 934, 1290, 1330, 1320]
            }
          ]
        },
        chartLineOut: null,
        chartBarOut: null,
        chartPieOut: null,
        chartScatterOut: null,
        optionOut: {
            title: {
              text: '消费(单位:元/月)'
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
              text: '收入(单位:元/月)'
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
    },
    methods: {
      // 消费折线图
      initChartLineOut () {
        this.chartLineOut = echarts.init(document.getElementById('J_chartLineBoxOut'))
        //发送请求获取当前节点最新的数据
        this.$http({
          url: this.$http.adornUrl('/booking/record/basicLineChartOut'),
          method: "get",
          params: {"type":"mouth","inOut": "支出"}
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

      // 消费折线图
      initChartLineIn () {
        this.chartLineIn = echarts.init(document.getElementById('J_chartLineBoxIn'))        
        this.$http({
          url: this.$http.adornUrl('/booking/record/basicLineChartOut'),
          method: "get",
          params: {"type":"mouth","inOut": "收入"}
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

      // 多数据折线图
        initChartLine () {
        this.chartLine = echarts.init(document.getElementById('J_chartLineBox'))        
        this.$http({
        url: this.$http.adornUrl('/booking/record/basicLineChartOut'),
        method: "get",
        params: {"type":"mouth","inOut": "支出"}
        })
        .then(({ data }) => {
          // for(var i=0;i<data.data.name.length;i++){
          //   this.optionIn.xAxis.data.push(data.data.name[i]);
          // }
          // for(var i=0;i<data.data.data.length;i++){
          //   this.optionIn.series[0].data.push(data.data.data[i]);
          // }

          this.chartLine.setOption(this.option)
        }).catch(() => {});

        window.addEventListener('resize', () => {
          this.chartLine.resize()
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
