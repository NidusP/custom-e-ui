<template>
  <div style="margin: 20px; display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap; background-color: darkseagreen">
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" custom placeholder="请输入内容"></el-input>
    <el-input v-model="input" custom placeholder="请输入内容">
      <template slot="prepend">关键词</template>
    </el-input>
    <el-button type="primary">buttonCont</el-button>
    <el-button type="primary">buttonCont</el-button>
    <el-button type="primary" color-type="warning">buttonCont</el-button>
    <el-button type="linear" color-type="danger">buttonCont</el-button>
    <el-button type="linear" color-type="warning">buttonCont</el-button>
    <el-button type="linear" color-type="warning" disabled>buttonCont</el-button>
    <el-button type="linear">buttonCont</el-button>

    <el-select v-model="input">
      <el-option v-for="item in option" :label="item.value" :value="item.value"></el-option>
    </el-select>

  </div>
</template>

<script>
  export default {
    data() {
      return {
        input: 'Hello Element UI!',
        option: [
          {
            label: '132',
            value: '123'
          },
          {
            label: '132',
            value: '123'
          },
          {
            label: '132',
            value: '123'
          }
        ]
      };
    }
  };
</script>
