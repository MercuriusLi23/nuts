<template>
  <div class="numberPad">
    <div class="output">{{ output }}</div>
    <div class="buttons">
      <button @click="inputContent">1</button>
      <button @click="inputContent">2</button>
      <button @click="inputContent">3</button>
      <button @click="add">+</button>
      <button @click="inputContent">4</button>
      <button @click="inputContent">5</button>
      <button @click="inputContent">6</button>
      <button @click="minus">-</button>
      <button @click="inputContent">7</button>
      <button @click="inputContent">8</button>
      <button @click="inputContent">9</button>
      <button @click="ok" class="ok">完成</button>
      <button class="zero" @click="inputContent">0</button>
      <button @click="inputContent">.</button>
      <button @click="remove">删除</button>
    </div>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';

@Component
export default class NumberPad extends Vue {
  @Prop() readonly value!: number;
  output = '';
  mounted(){
    this.output = this.value.toString();
  }

  inputContent(event: MouseEvent) {
    const button = (event.target as HTMLButtonElement); //强制指定类型
    const input = button.textContent!;
    if (this.output.length === 16) {return;}
    if (this.output === '0') {
      if (input === '0') {
        return;
      }
      if ('0123456789'.indexOf(input) >= 0) {
        this.output = input;
      } else {
        this.output += input;
      }
      return;
    }
    if (this.output.indexOf('.') >= 0) {
      if (input === '.') {
        return;
      }
    }
    this.output += input;
  }

  add() {}

  minus() {

  }

  remove() {
    if(this.output.length === 1){
      this.output = '0';
    }else{
        this.output = this.output.slice(0,-1);
      }
  }

  ok(){
    this.$emit('update:value',this.output);
    this.$emit('submit',this.output);
    this.output = '0';
  }
}
</script>

<style lang='scss' scoped>
@import '~@/assets/style/helper.scss';

.numberPad {

  .output {
    @extend %clearFix;
    @extend %innerShadow;
    font-size: 36px;
    font-family: Consolas, monospace; //编程等宽字体
    padding: 9px 16px;
    text-align: right;
    height: 72px;
  }

  .buttons {
    @extend %clearFix;

    > button {
      float: left;
      width: 25%;
      height: 64px;
      background: transparent;
      border: none;

      &.ok {
        height: 64*2px;
        float: right;
      }

      $bg: #f2f2f2;

      &:nth-child(1) {
        background: $bg;
      }

      &:nth-child(2), &:nth-child(5) {
        background: darken($bg, 4%); //颜色加深百分之四
      }

      &:nth-child(3), &:nth-child(6), &:nth-child(9) {
        background: darken($bg, 4*2%);
      }

      &:nth-child(4), &:nth-child(7), &:nth-child(10), &:nth-child(13) {
        background: darken($bg, 4*3%);
      }

      &:nth-child(8), &:nth-child(11), &:nth-child(14) {
        background: darken($bg, 4*4%);
      }

      &:nth-child(12) {
        background: darken($bg, 4*6%);
      }

      &:nth-child(15) {
        background: darken($bg, 4*5%);
      }
    }
  }
}
</style>