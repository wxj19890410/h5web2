<template>
  <div style="height:100%;width:100%;">
    <Sidebar/>
    <div style="" ref="openWindow" class="component-page"   >
      <el-upload
        class="upload-demo"
        drag
        :action="uploadUrl"
        :headers="headers"
        :data="upLoadData"
        :on-success="uploadImg"
        multiple>
        <i class="el-icon-upload"></i>
        <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
        <div class="el-upload__tip" slot="tip">只能上传xlsx/text文件，且不超过500kb</div>
      </el-upload>
      <!-- 筛选 -->

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
        <el-button icon="el-icon-search"  @click = "searchData()" circle></el-button>
      </div>

      <div style="width:100%;margin-left:0%;">
        <template >
          <el-table
            :data="tableData"
            stripe
            border
            :default-sort = "{prop: 'date', order: 'descending'}"
            >
            <el-table-column
              prop="month"
              label="日期"
              sortable
              >
            </el-table-column>
            <el-table-column
              prop="userName"
              label="姓名"
              >
            </el-table-column>
            <el-table-column
              prop="read"
              sortable
              label="读书指数">
            </el-table-column>
            <el-table-column
              prop="study"
              sortable
              label="学习成长">
            </el-table-column>
            <el-table-column
              prop="attendance"
              sortable
              label="出勤指数">
            </el-table-column>
            <el-table-column
              prop="hse"
              sortable
              label="HSE">
            </el-table-column>
            <el-table-column
              prop="culture"
              sortable
              label="企业文化">
            </el-table-column>
            <el-table-column
              label="精益改善"
              prop="improve">
            </el-table-column>
            <el-table-column label="操作">
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
              </template>
            </el-table-column>
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
      uploadUrl: '/huoli/file/upload',
      headers: {
        loginUuid: this.$service.localStorage.get('loginUuid')
      },
      upLoadData: {month: this.$store.state.today.month},
      pageSize: 10,
      time: this.$store.state.today.month,
      tableData0:{date: '2016-05-02',Name: '王小虎',Reading: 11,Study:22,Attendance:23,HSE:91,Culture:96,Attendance:35,},
      tableData: [],
      count: 0,
      valueMonth: this.$store.state.today.monthDate,
      inputSearch:'',
      currentPage:1,
    }
  },
  created () {
    this.getResturants()
  },
  mounted(){
    $(".component-page").width($(window).width()-240)
    $(".component-page").height($(window).height()-120)
    this.animatePage()
  },
  watch:{
    valueMonth:function(){
      var datetime=this.valueMonth.getFullYear() + '年' + (this.valueMonth.getMonth() + 1) +"月"
      this.time = datetime
      this.upLoadData.month = this.time
      this.getResturants()
    }
  },
  methods:{
    searchData () {
      this.getResturants()
    },
    getResturants() {
      const params = {}
      params.month = this.time
      params.inputSearch = this.inputSearch
      params.start = (this.currentPage - 1) * this.pageSize
      params.length = this.pageSize
      //展示源数据
      this.$http.get('/huoli/data/dataDataGrid', {params: params}).then(({ data }) => {
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
    uploadImg (res, file) {
      if (res.id) {
        this.getResturants()
      } else {
        this.$message.error('上传图片失败！')
      }
    },
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
    handleDelete(index, row) {
      console.log(index, row);
    },
    handleEdit(index, row) {
      console.log(index, row);
      var that = this
      const h = this.$createElement;
        this.$msgbox({
          title: '修改',
          message: "<div><span style='width:100px;display: inline-block;text-align: right;height:40px;line-height:40px;margin-right:20px;'>日期:</span><input disabled value='"  +that.tableData0.date  +"' style='height:30px;border:1px solid #878A90;border-radius:5px;padding:0 10px;color:#878A90;'></div>" + "<div><span style='width:100px;display: inline-block;text-align: right;height:40px;line-height:40px;margin-right:20px;'>姓名:</span><input disabled value='"  +that.tableData0.Name  +"' style='height:30px;border:1px solid #878A90;border-radius:5px;padding:0 10px;color:#878A90;'></div>"+"<div><span style='width:100px;display: inline-block;text-align: right;height:40px;line-height:40px;margin-right:20px;'>读书指数:</span><input value='"  +that.tableData0.Reading  +"' style='height:30px;border:1px solid #878A90;border-radius:5px;padding:0 10px;color:#878A90;'></div>" + "<div><span style='width:100px;display: inline-block;text-align: right;height:40px;line-height:40px;margin-right:20px;'>学习成长:</span><input value='"  +that.tableData0.Study  +"' style='height:30px;border:1px solid #878A90;border-radius:5px;padding:0 10px;color:#878A90;'></div>" + "<div><span style='width:100px;display: inline-block;text-align: right;height:40px;line-height:40px;margin-right:20px;'>出勤指数:</span><input value='"  +that.tableData0.Attendance  +"' style='height:30px;border:1px solid #878A90;border-radius:5px;padding:0 10px;color:#878A90;'></div>" + "<div><span style='width:100px;display: inline-block;text-align: right;height:40px;line-height:40px;margin-right:20px;'>HSE:</span><input value='"  +that.tableData0.HSE  +"' style='height:30px;border:1px solid #878A90;border-radius:5px;padding:0 10px;color:#878A90;'></div>"+"<div><span style='width:100px;display: inline-block;text-align: right;height:40px;line-height:40px;margin-right:20px;'>企业文化:</span><input value='"  +that.tableData0.Culture  +"' style='height:30px;border:1px solid #878A90;border-radius:5px;padding:0 10px;color:#878A90;'></div>",
          dangerouslyUseHTMLString:true,
          // <el-form ref="ableData0" :model="tableData0" label-width="80px">
    //   <el-form-item label="活动名称">
    //     <el-input v-model="tableData0.Name"></el-input>
    //   </el-form-item>
    // </el-form>
          showCancelButton: true,
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          beforeClose: (action, instance, done) => {
            if (action === 'confirm') {
              instance.confirmButtonLoading = true;
              instance.confirmButtonText = '执行中...';
              setTimeout(() => {
                done();
                setTimeout(() => {
                  instance.confirmButtonLoading = false;
                }, 300);
              }, 3000);
            } else {
              done();
            }
          }
        }).then(action => {
          this.$message({
            type: 'info',
            message: 'action: ' + action
          });
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tan-name{width:50px;display: inline-block;text-align: right;}
.shaixuan{display: flex;width: 50%;margin:50px 0 20px 0;}
</style>
