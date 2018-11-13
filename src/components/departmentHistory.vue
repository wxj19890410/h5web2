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
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" ><el-table-column prop="SubDepartment" label="子部门" sortable></el-table-column><el-table-column prop="DepNumber" label="部门人数" sortable></el-table-column><el-table-column prop="DepAverage"  label="部门总平均值" sortable></el-table-column><el-table-column prop="DepCulture" sortable  label="企业文化指数部门均值"></el-table-column><el-table-column prop="DepStudy" sortable label="学习成长指数部门均值"></el-table-column><el-table-column prop="DepChange"  label="精益改善指数部门均值" sortable></el-table-column><el-table-column prop="DepReading"  label="读书指数部门均值" sortable></el-table-column><el-table-column prop="DepHSE" sortable label="HSE指数部门均值"></el-table-column><el-table-column prop="DepAttendance" sortable label="出勤指数部门均值"></el-table-column><el-table-column prop="Date" sortable label="计算更新时间"></el-table-column>
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
      tableData: [{SubDepartment:"子部门1",DepNumber:"34",DepAverage:"67",DepCulture:"77",DepStudy:"88",DepChange:"99",DepReading:"45",DepHSE:"34",DepAttendance:"65",Date:"2018/05/12",},{SubDepartment:"子部门2",DepNumber:"34",DepAverage:"67",DepCulture:"77",DepStudy:"88",DepChange:"99",DepReading:"45",DepHSE:"34",DepAttendance:"65",Date:"2018/05/12",},{SubDepartment:"子部门3",DepNumber:"34",DepAverage:"67",DepCulture:"77",DepStudy:"88",DepChange:"99",DepReading:"45",DepHSE:"34",DepAttendance:"65",Date:"2018/05/12",},{SubDepartment:"子部门4",DepNumber:"34",DepAverage:"67",DepCulture:"77",DepStudy:"88",DepChange:"99",DepReading:"45",DepHSE:"34",DepAttendance:"65",Date:"2018/05/12",},{SubDepartment:"子部门5",DepNumber:"34",DepAverage:"67",DepCulture:"77",DepStudy:"88",DepChange:"99",DepReading:"45",DepHSE:"34",DepAttendance:"65",Date:"2018/05/12",},],
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
