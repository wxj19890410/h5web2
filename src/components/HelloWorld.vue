<template>
  <div style="height:100%;width:100%;">
    <Sidebar/>
    <div style="" ref="openWindow" class="component-page">
      <div class="title1">{{time}}各项指数统计  
        <div style="position:absolute;right:20px;top:0;">
          <el-date-picker
            v-model="valueMonth"
            type="month"
            placeholder="选择月">
          </el-date-picker>
        </div> 
      </div> 
      <div style="display:flex;justify-content:space-between;margin-bottom:30px;">
        <div id="myChart" :style="{width: '40%', height: '400px'}"></div>
        <div id="myChart2" :style="{width: '60%', height: '400px'}"></div>
      </div>
      <div class="title1">
        2018年各项指数值
        <div style="position:absolute;right:20px;top:0;">
          <el-date-picker
            v-model="valueYear"
            type="year"
            placeholder="选择年">
          </el-date-picker>
        </div>
      </div>
      <div style="display:flex;justify-content:space-between;margin-bottom:30px;">
        <div id="myChart3" :style="{width: '70%', height: '500px'}"></div>
        <div class="ranking-all">
          <div class="ranking-all-title" style=""><span>公司总排名</span><span>总值</span></div>
          <ul class="ranking-all-ul">
            <li v-for="(item,index) in 10" style="display:flex;justify-content:space-between;">
              <span>第{{index+1}}名： 李小花</span>
              <span>34</span>
            </li>
          </ul>
        </div>
      </div>
      <div class="title1" >7月部门排名  
        <div style="position:absolute;right:20px;top:0;">
          <el-date-picker
            v-model="valueMonth"
            type="month"
            placeholder="选择月">
          </el-date-picker>
        </div> 
      </div> 

      <div style="display:flex;justify-content:space-between;">
        <div style="border-radius:10px;overflow:hidden;border:1px solid #E9ECF3;width:48%;">
          <div class="part3-title" style="">生产部门</div>
          <template>
            <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" ><el-table-column prop="ID" label="排名" ></el-table-column><el-table-column prop="Name" label="姓名" ></el-table-column><el-table-column prop="Culture"  label="企业文化指数"></el-table-column><el-table-column prop="Study"  label="学习成长指数"></el-table-column><el-table-column prop="Change"  label="精益改善指数" ></el-table-column><el-table-column prop="Reading"  label="读书指数" ></el-table-column><el-table-column prop="HSE"  label="HSE指数"></el-table-column><el-table-column prop="Attendance"  label="出勤指数"></el-table-column><el-table-column prop="Average"  label="平均指数"></el-table-column>
            </el-table>
          </template>
        </div>
        <div style="border-radius:10px;overflow:hidden;border:1px solid #E9ECF3;width:48%;">
          <div class="part3-title" style="">非生产部门</div>
          <template>
            <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" ><el-table-column prop="ID" label="排名" ></el-table-column><el-table-column prop="Name" label="姓名" ></el-table-column><el-table-column prop="Culture"  label="企业文化指数"></el-table-column><el-table-column prop="Study"  label="学习成长指数"></el-table-column><el-table-column prop="Change"  label="精益改善指数" ></el-table-column><el-table-column prop="Reading"  label="读书指数" ></el-table-column><el-table-column prop="HSE"  label="HSE指数"></el-table-column><el-table-column prop="Attendance"  label="出勤指数"></el-table-column><el-table-column prop="Average"  label="平均指数"></el-table-column>
            </el-table>
          </template>
        </div>
      </div>
      <div class="title1" style="margin-top:50px;">
        班组活力指数走势图
        <div style="position:absolute;right:20px;top:0;">
          <el-select v-model="value" placeholder="请选择">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </div>
      </div>
      <div style="display:flex;justify-content:space-between;margin-bottom:30px;">
        <div id="myChart4" :style="{width: '60%', height: '500px'}"></div>
        <div id="myChart5" :style="{width: '40%', height: '600px'}"></div>
      </div>
      

    </div>
 
  </div>
</template>

<script>
import $ from 'jquery'

export default {
  name: 'HelloWorld',
  data () {
    return {
      time:"2018年7月",
      valueMonth:'',
      valueYear:'',
      tableData: [{ID:"第一名",Name:"王大妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第二名",Name:"王二妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第三名",Name:"王三妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第四名",Name:"王四妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第五名",Name:"王五妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第六名",Name:"王六妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第七名",Name:"王七妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第八名",Name:"王八妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第九名",Name:"王九妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},{ID:"第十名",Name:"王十妈",Culture:"45",Study:"65",Change:"76",Reading:"78",HSE:"32",Attendance:"45",Average:'66'},],
      options: [{
          value: '选项1',
          label: '班组1'
        }, {
          value: '选项2',
          label: '班组2'
        }, {
          value: '选项3',
          label: '班组3'
        }, {
          value: '选项4',
          label: '班组4'
        }, {
          value: '选项5',
          label: '班组5'
        }],
        value: '班组1'
    }
  },
  watch:{
    valueMonth:function(){
      var datetime=this.valueMonth.getFullYear() + '年' + (this.valueMonth.getMonth() + 1) +"月";
      console.log(datetime)
      this.time = datetime
      this.drawLine1();
      this.drawLine2();
      
    }
  },

  mounted(){
    $(".component-page").width($(window).width()-240)
    $(".component-page").height($(window).height()-120)
    this.animatePage();
    this.drawLine1();
    this.drawLine2();
    this.drawLine3();
    this.drawLine4();
    this.drawLine5();
  },
  methods:{
    changeMonth(){
      console.log(this.valueMonth)
    },
    animatePage(){
      $(".component-page").animate({
      　　"opacity":"1",
      　　"left":"220px"
      },500);
    },
    // 1
    drawLine1(){
      let myChart = this.$echarts.init(document.getElementById('myChart'))
      let option = {
        title : {
            text: this.time +'各项指数平均值',
            textStyle:{
              fontSize:16,
            },
            x:'center',
            top:0,
        },
        xAxis: {
            type: 'category',
            data: ['企业文化', '学习指数', '精益指数', '读书指数', 'HSE', '出勤指数', ],
            axisTick: {
                alignWithLabel: true
            }
        },
        yAxis: {
            type: 'value'
        },
        tooltip : {
        trigger: 'axis',
        axisPointer : {            // 坐标轴指示器，坐标轴触发有效
            type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        series: [{
            data: [12, 20, 15, 80, 70, 11,],
            type: 'bar',
            markLine: {
                data: [
                    {type: 'average', name: '平均值'}
                ]
            }
        }]
      };
      myChart.setOption(option);
    },
    // 2
    drawLine2(){
      let myChart2 = this.$echarts.init(document.getElementById('myChart2'))
      let option2 = {
        title : {
            text: this.time +'各项指数占比',
            x:'center',
            textStyle:{
              fontSize:16,
            },
            top:0,
        },
        tooltip : {
            trigger: 'item',
            formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
            type: 'scroll',
            orient: 'vertical',
            right: 10,
            top: 20,
            bottom: 20,
            data: ['企业文化', '学习指数', '精益指数', '读书指数', 'HSE', '出勤指数',],

            selected: ['企业文化', '学习指数', '精益指数', '读书指数', 'HSE', '出勤指数',],
        },
        series : [
            {
                name: '详情：',
                type: 'pie',
                radius : '55%',
                center: ['40%', '50%'],
                data: [ {value:33, name:'企业文化'},
                        {value:31, name:'学习指数'},
                        {value:23, name:'精益指数'},
                        {value:13, name:'读书指数'},
                        {value:15, name:'HSE'},
                        {value:15, name:'出勤指数'},
                      ],
                itemStyle: {
                    emphasis: {
                        shadowBlur: 10,
                        shadowOffsetX: 0,
                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                    }
                }
            }
        ]

      };
      myChart2.setOption(option2);
    },
    // 3
    drawLine3(){
      let myChart3 = this.$echarts.init(document.getElementById('myChart3'))
      let option3 = {
            
            tooltip: {
                trigger: 'axis'
            },
            legend: {
                data: ['企业文化', '学习指数', '精益指数', '读书指数', 'HSE', '出勤指数',],
            },
            toolbox: {
                show: true,
                feature: {
                    // dataZoom: {
                    //     yAxisIndex: 'none'
                    // },
                    // dataView: {readOnly: false},
                    magicType: {type: ['line', 'bar']},
                    restore: {},
                    saveAsImage: {}
                }
            },
            xAxis:  {
                type: 'category',
                boundaryGap: false,
                data: ['Jan','Feb','Mar','Apr','May','June','July','Aug','Sept','Oct','Nov','Dec']
            },
            yAxis: {
                type: 'value',
                axisLabel: {
                    formatter: '{value}'
                }
            },
            series: [
                {name:'企业文化',type:'line',data:[10, 21, 32, 41, 52, 61, 72,81,78,67,56,45],},
                {name:'学习指数',type:'line',data:[55, 55, 55, 55, 55, 55, 55,55,55,77,88,55],},
                {name:'精益指数',type:'line',data:[20, 31, 42, 51, 62, 71,82,91,88,77,66,55],},
                {name:'读书指数',type:'line',data:[11, 11, 11, 11, 11, 11, 11,11,11,11,11,11],},
                {name:'HSE',type:'line',data:[88, 77, 66, 55, 44, 33, 22,33,33,33,33,33],},
                {name:'出勤指数',type:'line',data:[15, 26, 35, 34, 47, 55, 51,61,32,44,38,29],},
            ]
        };
      myChart3.setOption(option3);
    },
    // 4
    drawLine4(){
      let myChart4 = this.$echarts.init(document.getElementById('myChart4'))
      let option4 = {
            
            tooltip: {
                trigger: 'axis'
            },
            legend: {
                data: ['企业文化', '学习指数', '精益指数', '读书指数', 'HSE', '出勤指数',],
            },
            toolbox: {
                show: true,
                feature: {
                    // dataZoom: {
                    //     yAxisIndex: 'none'
                    // },
                    // dataView: {readOnly: false},
                    magicType: {type: ['line', 'bar']},
                    restore: {},
                    saveAsImage: {}
                }
            },
            xAxis:  {
                type: 'category',
                boundaryGap: false,
                data: ['Jan','Feb','Mar','Apr','May','June','July','Aug','Sept','Oct','Nov','Dec']
            },
            yAxis: {
                type: 'value',
                axisLabel: {
                    formatter: '{value}'
                }
            },
            series: [
                {name:'企业文化',type:'line',data:[10, 21, 32, 41, 52, 61, 72,81,78,67,56,45],},
                {name:'学习指数',type:'line',data:[55, 55, 55, 55, 55, 55, 55,55,55,77,88,55],},
                {name:'精益指数',type:'line',data:[20, 31, 42, 51, 62, 71,82,91,88,77,66,55],},
                {name:'读书指数',type:'line',data:[11, 11, 11, 11, 11, 11, 11,11,11,11,11,11],},
                {name:'HSE',type:'line',data:[88, 77, 66, 55, 44, 33, 22,33,33,33,33,33],},
                {name:'出勤指数',type:'line',data:[15, 26, 35, 34, 47, 55, 51,61,32,44,38,29],},
            ]
        };
      myChart4.setOption(option4);
    },
    // 5
    drawLine5(){
      let myChart5 = this.$echarts.init(document.getElementById('myChart5'))
      let option5 = {
        title : {
            text: '班组各项指数占比',
            x:'center',
            textStyle:{
              fontSize:16,
            },
            top:0,
        },
        tooltip : {
            trigger: 'item',
            formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
            type: 'scroll',
            orient: 'vertical',
            right: 10,
            top: 20,
            bottom: 20,
            data: ['企业文化', '学习指数', '精益指数', '读书指数', 'HSE', '出勤指数',],

            selected: ['企业文化', '学习指数', '精益指数', '读书指数', 'HSE', '出勤指数',],
        },
        series : [
            {
                name: '详情：',
                type: 'pie',
                radius : '55%',
                center: ['40%', '50%'],
                data: [ {value:33, name:'企业文化'},
                        {value:31, name:'学习指数'},
                        {value:23, name:'精益指数'},
                        {value:13, name:'读书指数'},
                        {value:15, name:'HSE'},
                        {value:15, name:'出勤指数'},
                      ],
                itemStyle: {
                    emphasis: {
                        shadowBlur: 10,
                        shadowOffsetX: 0,
                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                    }
                }
            }
        ]

      };
      myChart5.setOption(option5);
    },
   
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.title1{text-align: center;font-size: 25px;font-weight: 800;border-bottom: 1px solid #B6B6B6;padding-bottom: 30px;margin-bottom: 30px;position: relative;}
.ranking-all{background-color: #4F77AB;color:#fff;width: 25%;border-radius: 20px;box-shadow: 0px 0px 10px rgba(0,0,0,0.9);padding:30px;height: 90%;}
.ranking-all-ul{width: 100%;padding:0;margin:0;}
.ranking-all-title{display:flex;justify-content:space-between;font-size: 18px;border-bottom: 1px solid #eee;margin-bottom: 10px;font-weight: 600;padding:0 5px 10px 5px;}
.ranking-all-ul li{height: 35px;line-height: 35px;cursor: pointer;padding:0 5px;}
.ranking-all-ul li:hover{
  background-color: #fff;
  color:#65737E;
}
.part3-title{background-color:#4F77AB;color:#fff;text-align:center;font-size:20px;padding:20px 0;font-weight:700;}
</style>
