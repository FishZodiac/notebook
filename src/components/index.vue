<template>
  <div class="hello">
    <Myheader></Myheader>
    <div class="container">
      <div class="list">
        <Mylist></Mylist>
      </div>
    </div>
  </div>
</template>

<script>
import Myheader from './Header'
import Mylist from './List'
export default {
  name: 'hello',
  components: {
    Myheader:Myheader,
    Mylist:Mylist
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container{padding: 10px}
  .text {
    font-size: 14px;
  }

  .item {
    padding: 18px 0;
  }

  .clearfix:before,
  .clearfix:after {
      display: table;
      content: "";
  }
  .clearfix:after {
      clear: both
  }

  .box-card {
    width: 480px;
  }
</style>
