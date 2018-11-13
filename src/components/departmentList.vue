<template>
  <div style="height:100%;width:100%;">
    <Sidebar/>
    <div style="" ref="openWindow" class="component-page">
      <div style="display:flex;justify-content:space-between;margin:50px 0 20px 0;">
        <div class="shaixuan">
          <div style="width:100px;margin-rignt:30px;color:#58595D;line-height:35px;">选择部门：</div>
          <el-select v-model="value" placeholder="请选择">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </div>
        <el-button type="primary" style="height:40px;" round>更新数据</el-button>
      </div>
      <div style="width:100%;margin-left:0%;">
        <template >
          <el-table :data="tableData" stripe border :default-sort = "{prop: 'date', order: 'descending'}" ><el-table-column prop="department" label="部门"></el-table-column><el-table-column prop="number" label="部门人数"></el-table-column><el-table-column prop="Date" sortable label="计算更新时间"></el-table-column>
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
      options: [{
        value: '选项1',
        label: '生产部门'
      }, {
        value: '选项2',
        label: '非生产部门'
      },],
      value: '生产部门',
      tableData: [{department:"管理部",number:'56',Date:"2018/04/14"},{department:"技术部",number:'56',Date:"2018/04/14"},{department:"市场部",number:'56',Date:"2018/04/14"},{department:"设计部",number:'56',Date:"2018/04/14"},{department:"管理部",number:'56',Date:"2018/04/14"},{department:"销售部",number:'56',Date:"2018/04/14"},{department:"货运部",number:'56',Date:"2018/04/14"},{department:"会计部",number:'56',Date:"2018/04/14"},],
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
