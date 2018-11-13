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
          <el-button icon="el-icon-search"  circle @click = "searchData()"></el-button>
        </div>
      </div>
      <div style="width:100%;margin-left:0%;">
        <template >
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" ><el-table-column prop="userid" label="系统id" ></el-table-column><el-table-column prop="name"  label="姓名"></el-table-column><el-table-column prop="mobile"  label="手机号码"></el-table-column><el-table-column prop="avatar"  label="微信头像"><template slot-scope="scope"><img  :src="scope.row.avatar" alt="" style="width: 40px;height: 40px"></template></el-table-column><el-table-column prop="SubDepartment"  label="主部门"></el-table-column><el-table-column prop="MainDepartment"  label="子部门"></el-table-column><el-table-column prop="Team"  label="班组"></el-table-column><el-table-column prop="SumRank" sortable label="总排名"></el-table-column><el-table-column prop="total" sortable label="总指数"></el-table-column><el-table-column prop="culture" sortable label="企业文化指数"></el-table-column><el-table-column prop="study" sortable label="学习成长指数"></el-table-column><el-table-column prop="improve" sortable label="精益改善指数"></el-table-column><el-table-column prop="read" sortable label="读书指数"></el-table-column><el-table-column prop="hse" sortable label="HSE指数"></el-table-column><el-table-column prop="attendance" sortable label="出勤指数"></el-table-column><el-table-column prop="Date" sortable label="计算更新时间"></el-table-column>
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
  name: 'systemList',
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
      params.inputSearch = this.inputSearch
      params.month = this.time
      params.avg = '1'
      params.start = (this.currentPage - 1) * this.pageSize
      params.length = this.pageSize
      this.$http.get('/huoli/user/userDataGrid', {params: params}).then(({ data }) => {
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
