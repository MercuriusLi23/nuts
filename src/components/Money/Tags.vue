<template>
  <div class="tags">
    <div class="new">
      <button @click="create">新增标签</button>
    </div>
    <ul class="current">
      <li v-for="tag in dataSource" :key="tag"
          :class="{selected: selectedTags.indexOf(tag) >= 0}"
      @click="toggle(tag)">{{tag}}</li>
    </ul>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';
@Component
export default class Tags extends Vue {
@Prop() readonly dataSource: string[] | undefined;  //注明为字符串数组,默认为空
selectedTags: string[] = [];

toggle(tag: string){
  const index = this.selectedTags.indexOf(tag);
  if(index>=0){
this.selectedTags.splice(index,1);
  }else{
    this.selectedTags.push(tag);
  }
this.$emit('update:value',this.selectedTags)
}
create() {
  const name = window.prompt('请输入标签名');
  if(name ===''){
    window.alert('标签名不能为空');
    }else{
if(this.dataSource) {
  this.$emit('update:dataSource',[...this.dataSource,name]);
}
  }

}
  }

</script>

<style lang='scss' scoped>
.tags {
  display: flex;
  flex-direction: column-reverse;
  flex-grow: 1;
  font-size: 14px;
  padding: 16px;
  > .current{
    display: flex;
    flex-wrap: wrap;
    > li{
      background: #d9d9d9;
      $h: 24px;
      height: $h;
      line-height: $h;
      border-radius: $h/3;
      padding: 0 16px;
      margin-right:12px;
      margin-top: 4px;
      &.selected {
        background: #daa520;
        color:white;
      }
    }
  }
  > .new{
    padding-top: 16px;
    button{
      background: transparent;
      border: none;
      color: #999;
      border-bottom: 1px solid;  //新增标签下的下划线
      padding: 0 4px;   //使得下划线比文字长度长一点
    }
  }
}
</style>