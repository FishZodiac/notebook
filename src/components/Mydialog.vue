<template>
	<div>
	<el-button class="addinfo" type="text" @click="dialogFormVisible = true"><i class="el-icon-plus"></i></el-button>
	<el-dialog title="我的笔记" size="large" :visible.sync="dialogFormVisible">
	  <el-form :model="form">
	    <el-form-item label="标题" :label-width="formLabelWidth">
	      <el-input v-model="form.name" auto-complete="off"></el-input>
	    </el-form-item>
	    <el-form-item label="简介" :label-width="formLabelWidth">
	      <el-input type="textarea" v-model="form.desc"></el-input>
	    </el-form-item>
	  </el-form>
	  <div slot="footer" class="dialog-footer">
	    <el-button @click="dialogFormVisible = false">取 消</el-button>
	    <el-button type="primary" @click="addNote">确 定</el-button>
	  </div>
	</el-dialog>
	</div>
</template>
<script>
  export default {
    data() {
      return {
        dialogFormVisible: false,
        form: {
          name: '',
          desc: ''
        },
        formLabelWidth: '50px'
      };
    },
    methods: {
    	addNote(){
    		var info = [];
    		var historyinfo = localStorage.getItem("info");
    		if (historyinfo) {
    			info = JSON.parse(historyinfo);
    		}
    		var _time = this.getNowFormatDate();
    		info.unshift({"name":this.form.name, "desc":this.form.desc,"time":_time});
    		localStorage.setItem("info",JSON.stringify(info));
    		this.$emit("refreshs");
    		this.dialogFormVisible =false;
    	},
    	getNowFormatDate() {
		    var date = new Date();
		    var seperator1 = "-";
		    var seperator2 = ":";
		    var month = date.getMonth() + 1;
		    var strDate = date.getDate();
		    if (month >= 1 && month <= 9) {
		        month = "0" + month;
		    }
		    if (strDate >= 0 && strDate <= 9) {
		        strDate = "0" + strDate;
		    }
		    var currentdate = date.getFullYear() + seperator1 + month + seperator1 + strDate
		            + " " + date.getHours() + seperator2 + date.getMinutes()
		            + seperator2 + date.getSeconds();
		    return currentdate;
		}
    }
  };
</script>
<style>
	.addinfo{position: fixed;right: 20px;bottom: 20px;background: #20a0ff;border-radius: 50%;padding: 20px;color: #fff;box-shadow: 1px 1px 1px rgba(0,0,0,0.2)}
	.el-dialog{border-radius: 5px}
</style>