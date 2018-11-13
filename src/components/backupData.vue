<template>
	<div style="height:100%;width:100%;">
	    <Sidebar/>
	    <div style="" ref="openWindow" class="component-page"> 
	    	<div style="padding:20px;border-bottom:1px solid #B6B6B6;margin-bottom:50px;">
	    		<el-button type="primary" plain>备份当前数据</el-button>
	    	</div>

	    	<template>
			    <el-table
			      :data="tableData"
			      style="width: 100%">
			      <el-table-column
			        prop="name"
			        label="文件名"
			        width="180">
			      </el-table-column>
			      <el-table-column
			        prop="date"
			        label="日期"
			        width="180">
			      </el-table-column>
			      <el-table-column label="操作">
				      <template slot-scope="scope">
				        <el-button
				          size="mini"
				          @click="handleEdit(scope.$index, scope.row)">上传</el-button>
				      </template>
				    </el-table-column>
			    </el-table>
			</template>

	    </div>
    </div>
</template>

<script>
import $ from 'jquery'
export default {
  name: 'backupData',
  data () {
    return {
    	tableData: [{
            date: '2016-05-02',
            name: 'beifen.text',
          }]
    
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
    handleEdit(index, row) {
	    console.log(index, row);
	},
   }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.component-page{height:300px;width:400px;box-shadow: 0px 0px 10px rgba(0,0,0,0.5); position:absolute;top:80px;left:150px;border-radius: 10px;background-color: #fff;opacity: 0;padding:50px;overflow-y: scroll;}

</style>
