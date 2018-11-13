<template>
  <div style="height:100%;width:100%;">
    <Sidebar/>
    <div style="" ref="openWindow" class="component-page">
      <div style="display:flex;justify-content:space-between;margin:50px 0 20px 0;">
        <div class="shaixuan">
          <div style="width:100px;margin-rignt:30px;color:#58595D;line-height:35px;">筛选：</div>
          <el-input
            placeholder="请输入内容"
            v-model="inputSearch"
            style="margin-right:30px;"
            clearable>
          </el-input>
          <el-date-picker
            v-model="valueMonth"
            type="month"
            style="margin-right:30px;"
            placeholder="选择月">
          </el-date-picker>
          <el-button icon="el-icon-search"  circle></el-button>
        </div>
        <el-button type="primary" style="height:40px;" round>更新数据</el-button>
      </div>
      <div style="width:100%;margin-left:0%;">
        <template >
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" ><el-table-column prop="SumAverage" label="公司平均值" sortable></el-table-column><el-table-column prop="Sum" label="总指数" sortable></el-table-column><el-table-column prop="CountedAmount"  label="统计公司总人数" sortable></el-table-column><el-table-column prop="CultureAverage" sortable  label="企业文化平均指数"></el-table-column><el-table-column prop="StudyAverage" sortable label="学习成长平均指数"></el-table-column><el-table-column prop="ChangeAverage"  label="精益改善平均指数" sortable></el-table-column><el-table-column prop="ReadingAverage"  label="读书平均指数" sortable></el-table-column><el-table-column prop="HSEAverage" sortable label="HSE平均指数"></el-table-column><el-table-column prop="AttendanceAverage" sortable label="出勤平均指数"></el-table-column><el-table-column prop="Date" sortable label="计算更新时间"></el-table-column>
          </el-table>
        </template>
      </div>
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        style="margin-top:20px;"
        :page-sizes="[2, 4, 6, 8]"
        :page-size="100"
        layout="total, sizes, prev, pager, next, jumper"
        :total="tableData.length">
      </el-pagination>
 
    </div>
 
  </div>
</template>

<script>
import $ from 'jquery'

export default {
  name: 'totalHistory',
  data () {
    return {
      tableData: [{SumAverage:"56",Sum:"45",CountedAmount:"666",CultureAverage:"45",StudyAverage:"44",ChangeAverage:"34",ReadingAverage:"54",HSEAverage:"65",AttendanceAverage:"67",Date:"2018/04/14"},{SumAverage:"56",Sum:"45",CountedAmount:"666",CultureAverage:"45",StudyAverage:"44",ChangeAverage:"34",ReadingAverage:"54",HSEAverage:"65",AttendanceAverage:"67",Date:"2018/04/14"},{SumAverage:"56",Sum:"45",CountedAmount:"666",CultureAverage:"45",StudyAverage:"44",ChangeAverage:"34",ReadingAverage:"54",HSEAverage:"65",AttendanceAverage:"67",Date:"2018/04/14"},{SumAverage:"56",Sum:"45",CountedAmount:"666",CultureAverage:"45",StudyAverage:"44",ChangeAverage:"34",ReadingAverage:"54",HSEAverage:"65",AttendanceAverage:"67",Date:"2018/04/14"},{SumAverage:"56",Sum:"45",CountedAmount:"666",CultureAverage:"45",StudyAverage:"44",ChangeAverage:"34",ReadingAverage:"54",HSEAverage:"65",AttendanceAverage:"67",Date:"2018/04/14"},{SumAverage:"56",Sum:"45",CountedAmount:"666",CultureAverage:"45",StudyAverage:"44",ChangeAverage:"34",ReadingAverage:"54",HSEAverage:"65",AttendanceAverage:"67",Date:"2018/04/14"},],
      valueMonth:'',
      inputSearch:'',
      currentPage:2,
    
    }
  },
  mounted(){
    $(".component-page").width($(window).width()-240)
    $(".component-page").height($(window).height()-120)
    this.animatePage()
  },
  methods:{
    animatePage(){
      $(".component-page").animate({
      　　"opacity":"1",
      　　"left":"220px"
      },500);
    },
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.shaixuan{display: flex;width: 50%;}
</style>
