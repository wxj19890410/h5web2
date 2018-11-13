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
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" ><el-table-column prop="ImportTime" label="导入时间" sortable ></el-table-column><el-table-column prop="Acount" label="导入账号" ></el-table-column><el-table-column prop="ImportIP"  label="导入IP"></el-table-column><el-table-column prop="CountTime"  label="计算时间" sortable></el-table-column><el-table-column prop="Status" sortable label="状态"></el-table-column>
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
  name: 'systemList',
  data () {
    return {
      tableData: [{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},{ImportTime:"2018/01/25",Acount:"12525652365",ImportIP:"123456",CountTime:"1000",Status:"1",},],
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
