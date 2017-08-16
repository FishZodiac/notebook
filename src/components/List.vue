<template>
<div>
<Search @filters="filterInfo"></Search>
<el-collapse accordion class="listContent">
  <el-collapse-item class="list_item" v-onHold="{refreshs:refresh}" :data-id="item.name" v-for="item in items" :key="item.time">
    <template slot="title">
      {{item.name}}<i class="time">{{item.time}}</i>
    </template>
    <div>{{item.desc}}</div>
  </el-collapse-item>
</el-collapse>
<Mydialog @refreshs="refresh"></Mydialog>
</div>
</template>  
<script>
import Mydialog from './Mydialog'
import Search from './Search'
  export default {
    data() {
      return {
        items: []    
      };
    },
    components:{
          Mydialog:Mydialog,
          Search:Search,
    },
    mounted: function () {
    // `this` 指向 vm 实例
     this.items = JSON.parse(localStorage.getItem('info'));
    },
    methods:{
      refresh(){
        this.items = JSON.parse(localStorage.getItem('info'));
      },
      filterInfo(newV){
        var _items = JSON.parse(localStorage.getItem('info'));
        var _newItem = [];
        for(var k in _items){
          if (_items[k].name.indexOf(newV)>-1) {
            _newItem.push(_items[k]);
            continue;            
          }
        }
        this.items = _newItem;
      },
    },
    directives:{
      onHold:{
        bind(el,binding){
          var timer,
              timeing = 1;
          el.addEventListener("touchstart",function(e){
            timer =  setInterval(function() {
              timeing++;
            }, 1000);
          });
          el.addEventListener("touchend",function(e){
            if (timeing>2) {
              e.preventDefault();
              e.stopPropagation();
              var _name = el.getAttribute("data-id");
              var _items = JSON.parse(localStorage.getItem('info'));
              for(var k in _items){
                if (_items[k].name == _name){
                  _items.splice(k,1);
                  break;            
                }
              }
              localStorage.setItem("info",JSON.stringify(_items));
              binding.value.refreshs();
            }
            clearInterval(timer);
            timeing=1;            
          })
        }
      }
    }
  }
</script>
<style scoped>
  .listContent{margin: 10px 0;}
  .list_item{text-align: left;}
  .list_item .time{float: right;margin-right: 8px}
</style>