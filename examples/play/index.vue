<template>
  <div style="margin: 20px; display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap; background-color: darkseagreen">
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-button type="primary">buttonCont</el-button>
    <el-button type="primary">buttonCont</el-button>
    <el-button type="primary">buttonCont</el-button>
    <el-button type="primary">buttonCont</el-button>
    <el-button type="primary">buttonCont</el-button>

    <el-button type="linear">buttonCont</el-button>

    《》
  </div>
</template>

<script>
  export default {
    data() {
      return {
        input: 'Hello Element UI!'
      };
    }
  };
</script>
