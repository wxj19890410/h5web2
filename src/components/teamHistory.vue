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
          <el-button icon="el-icon-search"  @click = "searchData()" circle ></el-button>
        </div>
        <el-button type="primary" style="height:40px;" round>更新数据</el-button>
      </div>
      <div style="width:100%;margin-left:0%;">
        <template >
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" >
            <el-table-column prop="name" label="班组" sortable></el-table-column>
            <el-table-column prop="number" label="班组人数" sortable></el-table-column>
            <el-table-column prop="total"  label="班组总平均值" sortable></el-table-column>
            <el-table-column prop="culture" sortable  label="企业文化指数部门均值"></el-table-column>
            <el-table-column prop="study" sortable label="学习成长指数部门均值"></el-table-column>
            <el-table-column prop="improve"  label="精益改善指数部门均值" sortable></el-table-column><el-table-column prop="read"  label="读书指数部门均值" sortable></el-table-column>
            <el-table-column prop="hse" sortable label="HSE指数部门均值"></el-table-column>
            <el-table-column prop="attendance" sortable label="出勤指数部门均值"></el-table-column><el-table-column prop="Date" sortable label="计算更新时间"></el-table-column>
          </el-table>
        </template>
      </div>
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        style="margin-top:20px;"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="count">
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
      count: 0,
      pageSize: 20,
      currentPage: 1,
      tableData: [],
      valueMonth:'',
      inputSearch:'',
      time: ''
    }
  },
  mounted(){
    $(".component-page").width($(window).width()-240)
    $(".component-page").height($(window).height()-120)
    this.animatePage()
  },
  created () {
    this.initData()
  },
  watch:{
    valueMonth:function(){
      var datetime=this.valueMonth.getFullYear() + '年' + (this.valueMonth.getMonth() + 1) +"月"
      this.time = datetime
    }
  },
  methods:{
    searchData () {
      this.initData()
    },
    initData () {
      const params = {}
      params.month = this.time
      params.inputSearch = this.inputSearch
      params.start = (this.currentPage - 1) * this.pageSize
      params.length = this.pageSize
      this.$http.get('/huoli/org/groupDataGrid', {params: params}).then(({ data }) => {
        if (data) {
          this.tableData = data.rows
          this.count = data.count
        } else {
          this.$message({
            type: 'error',
            message: data.message
          })
        }
      })
    },
    animatePage(){
      $(".component-page").animate({
      　　"opacity":"1",
      　　"left":"220px"
      },500);
    },
    handleSizeChange (val) {
      this.currentPage = val
      this.initData()
    },
    handleCurrentChange (val) {
      this.currentPage = val
      this.initData()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.shaixuan{display: flex;width: 50%;}
</style>
