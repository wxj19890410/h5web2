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
          <el-button icon="el-icon-search"  circle></el-button>
        </div>
      </div>
      
      <div style="width:100%;margin-left:0%;">
        <template >
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" >
            <el-table-column prop="OpenID" label="部门" >
              <template slot-scope="scope">
                <el-switch
                  @change="switchChange(scope.row)"
                  v-model="scope.row.OpenID"
                  active-text="生产"
                  inactive-text="非生产"
                  active-value="01"
                  inactive-value="02">
                </el-switch>
              </template>           
            </el-table-column>
           <!--  <el-table-column prop="OpenID" label="微信id" sortable></el-table-column> -->
            <el-table-column prop="WeName" label="微信昵称" ></el-table-column>
            <el-table-column prop="Name" sortable label="姓名"></el-table-column>
            <el-table-column prop="PhoneNumber" sortable label="手机号码">
            </el-table-column>
            <el-table-column prop="WeImage" sortable label="微信头像">
              <template slot-scope="scope"><img  :src="scope.row.WeImage" alt="" style="width: 40px;height: 40px"></template></el-table-column>
            <el-table-column prop="ID" sortable label="系统id"></el-table-column>
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
  name: 'wechatsList',
  data () {
    return {
      tableData: [{OpenID: '02',WeName: '蟹黄汤包来十笼',Name: "王大牛",PhoneNumber:"12121212121",WeImage:"/static/weUrl.png",ID:"1"},{OpenID: '01',WeName: '蟹黄汤包来十笼',Name: "王大牛",PhoneNumber:"12121212121",WeImage:"/static/weUrl.png",ID:"1"},{OpenID: '123526525',WeName: '蟹黄汤包来十笼',Name: "王大牛",PhoneNumber:"12121212121",WeImage:"/static/weUrl.png",ID:"1"},{OpenID: '123526525',WeName: '蟹黄汤包来十笼',Name: "王大牛",PhoneNumber:"12121212121",WeImage:"/static/weUrl.png",ID:"1"},{OpenID: '123526525',WeName: '蟹黄汤包来十笼',Name: "王大牛",PhoneNumber:"12121212121",WeImage:"/static/weUrl.png",ID:"1"},{OpenID: '123526525',WeName: '蟹黄汤包来十笼',Name: "王大牛",PhoneNumber:"12121212121",WeImage:"/static/weUrl.png",ID:"1"},{OpenID: '123526525',WeName: '蟹黄汤包来十笼',Name: "王大牛",PhoneNumber:"12121212121",WeImage:"/static/weUrl.png",ID:"1"},{OpenID: '123526525',WeName: '蟹黄汤包来十笼',Name: "王大牛",PhoneNumber:"12121212121",WeImage:"/static/weUrl.png",ID:"1"}, ],
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
    switchChange(data, data2) {
      console.log(data)
      console.log(data2)

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
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.shaixuan{display: flex;width: 50%;}
</style>
