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
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" ><el-table-column prop="Team" label="班组" sortable></el-table-column><el-table-column prop="TeamNumber" label="班组人数" sortable></el-table-column><el-table-column prop="TeamAverage"  label="班组总平均值" sortable></el-table-column><el-table-column prop="TeamCulture" sortable  label="企业文化指数班组均值"></el-table-column><el-table-column prop="TeamStudy" sortable label="学习成长指数班组均值"></el-table-column><el-table-column prop="TeamChange"  label="精益改善指数班组均值" sortable></el-table-column><el-table-column prop="TeamReading"  label="读书指数班组均值" sortable></el-table-column><el-table-column prop="TeamHSE" sortable label="HSE指数班组均值"></el-table-column><el-table-column prop="TeamAttendance" sortable label="出勤指数班组均值"></el-table-column><el-table-column prop="Date" sortable label="计算更新时间"></el-table-column>
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
  name: 'departmentList',
  data () {
    return {
      tableData: [{Team:"班组1",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组2",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组4",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组3",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组6",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组5",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组7",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组8",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组9",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组11",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},{Team:"班组10",TeamNumber:"34",TeamAverage:"67",TeamCulture:"77",TeamStudy:"88",TeamChange:"99",TeamReading:"45",TeamHSE:"34",TeamAttendance:"65",Date:"2018/05/12",},],
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
