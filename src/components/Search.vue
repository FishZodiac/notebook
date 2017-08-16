<template>
	<el-input v-model="input" placeholder="搜索"></el-input>
</template>
<script>
export default {
  data() {
    return {
      input: ''
    }
  },
  watch: {
  	input(newV,oldV){
  		if (newV != oldV) {
  			this.$emit("filters",newV);
  		}
  	}
  }
}
</script>