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
          <el-button icon="el-icon-search"  circle  @click = "searchData()"></el-button>
        </div>
      </div>
      
      <div style="width:100%;margin-left:0%;">
        <template >
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" >
            <el-table-column prop="ignoreFlag" label="推送消息" >
              <template slot-scope="scope">
                <el-switch
                  @change="switchChange(scope.row)"
                  v-model="scope.row.ignoreFlag"
                  active-text="不发送"
                  inactive-text="发送"
                  active-value="1"
                  inactive-value="0">
                </el-switch>
              </template>           
            </el-table-column>
           <!--  <el-table-column prop="OpenID" label="微信id" sortable></el-table-column> -->
    <!--         <el-table-column prop="WeName" label="微信昵称" ></el-table-column> -->
            <el-table-column prop="name" sortable label="姓名"></el-table-column>
            <el-table-column prop="mobile" sortable label="手机号码">
            </el-table-column>
            <el-table-column prop="position" label="职位" ></el-table-column>
            <el-table-column prop="avatar" sortable label="微信头像">
              <template slot-scope="scope"><img  :src="scope.row.avatar" alt="" style="width: 40px;height: 40px"></template></el-table-column>
            <el-table-column prop="userid" sortable label="系统id"></el-table-column>
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
  name: 'wechatsList',
  data () {
    return {
      count: 0,
      pageSize: 20,
      currentPage: 1,
      tableData: [],
      inputSearch:''
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
  methods:{
    searchData () {
      this.initData()
    },
    initData () {
      const params = {}
      params.inputSearch = this.inputSearch
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
    switchChange (data) {
      const params = {}
      params.userid = data.userid
      params.ignoreFlag = data.ignoreFlag
      this.$http.get('/huoli/user/setIgnoreFlag', {params: params}).then(({ data }) => {
        if (data) {
          console.log(data)
          // this.initData()
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
