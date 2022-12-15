<template>
  <Layout>
    <div class="tags">
      <ul class="current">
        <li>衣</li>
        <li>食</li>
        <li>住</li>
        <li>行</li>
      </ul>
      <div class="new">
        <button>新增标签</button>
      </div>
    </div>

    <div>
      <label class="notes">
        <spen class="name">备注</spen>
        <input type="text">
      </label>
    </div>
    
    <div>
      <ul class="types">
        <li class="selected">支出</li>
        <li>收入</li>
      </ul>
    </div>

    <div class="numberPad">
      <div class="output">100</div>
      <div class="buttons">
        <bitton>1</bitton>
        <bitton>2</bitton>
        <bitton>3</bitton>
        <bitton>+</bitton>
        <bitton>4</bitton>
        <bitton>5</bitton>
        <bitton>6</bitton>
        <bitton>-</bitton>
        <bitton>7</bitton>
        <bitton>8</bitton>
        <bitton>9</bitton>
        <bitton>.</bitton>
        <bitton>0</bitton>
        <bitton>/</bitton>
        <bitton>完成</bitton>
      </div>
    </div>
  </Layout>
</template>

<script lang="ts">
export default {
  name: 'Money'
};
</script>
