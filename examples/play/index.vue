<template>
  <div style="margin: 20px; display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap; background-color: olivedrab">
    <el-input v-model="input" placeholder="请输入内容" custom prefix-label="关键词213"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>

    <el-input v-model="input" custom style="height: 40px; line-height: 40px">
      <template slot="tip">
        <label class="el-input__tip-inner" alt='请输入密码' placeholder='密码'></label>
      </template>
    </el-input>

    <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" class="demo-ruleForm custom-style" :show-message="false">
      <el-form-item  prop="username">
        <el-input name="username" v-model.number="ruleForm.username" placeholder="asd"></el-input>
        <label class="tip" alt='请输入用户名' placeholder='用户名' ref="tips-user"></label>
      </el-form-item>
      <el-form-item prop="password">
        <el-input v-model="ruleForm.password" custom style="height: 36px; line-height: 36px">
          <template slot="tip">
            <label class="el-input__tip-inner" alt='请输入密码' placeholder='密码'></label>
          </template>
        </el-input>
      </el-form-item>
      <el-form-item prop="password">
        <el-input name="password" type="password" v-model="ruleForm.password" autocomplete="off"></el-input>
        <label class="tip" alt='请输入密码' placeholder='密码' ref="tips-pass"></label>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" size="mini" :loading="doAjax">登录</el-button>
      </el-form-item>
    </el-form>



    <el-input v-model="input" custom placeholder="请输入内容"></el-input>
    <el-input v-model="input" custom placeholder="请输入内容">
      <template slot="label">关键词</template>
    </el-input>
    <el-button type="primary">buttonCont</el-button>
    <el-button type="primary">buttonCont</el-button>
    <el-button type="primary" color-type="warning">buttonCont</el-button>
    <el-button type="linear" color-type="danger">buttonCont</el-button>
    <el-button type="linear" color-type="warning">buttonCont</el-button>
    <el-button type="linear" color-type="warning" disabled>buttonCont</el-button>
    <el-button type="linear">buttonCont</el-button>

    <el-select v-model="select" multiple filterable>
      <el-option v-for="(item, index) in option" :key="index" :label="item.value" :value="item.value"></el-option>
    </el-select>

    <el-select v-model="select" custom prefix-label="关键词1" multiple filterable>
      <el-option v-for="(item, index) in optionEmpty" :key="index" :label="item.value" :value="item.value"></el-option>
    </el-select>

    <el-select v-model="input" custom  :popper-append-to-body="false">
      <el-option v-for="(item, index) in option" :key="index" :label="item.value" :value="item.value"></el-option>
    </el-select>
  </div>
</template>

<script>
  export default {
    data() {
      const checkAge = (rule, value, callback) => {
        if (!value.trim()) {
          this.$refs['tips-user'].style.color = '#F56C6C'
          return callback(new Error('请输入用户名'));
        }  else {
          callback();
        }
      };
      const validatePass = (rule, value, callback) => {
        if (!value.trim()) {
          this.$refs['tips-pass'].style.color = '#F56C6C'
          callback(new Error('请输入密码'));
        }  else {
          callback();
        }
      };
      return {
        input: '',
        select: [],
        doAjax: '',
        ruleForm: {
          password: '',
          username: ''
        },
        rules: {
          password: [
            { validator: validatePass, trigger: 'blur' }
          ],
          username: [
            { validator: checkAge, trigger: 'blur' }
          ]
        },
        option: [
          {
            label: '132',
            value: '123'
          },
          {
            label: '132',
            value: '1234'
          },
          {
            label: '132',
            value: '1235'
          }
        ],
        optionEmpty: []
      };
    }
  };
</script>
<style scoped lang="scss">
  .demo-ruleForm {
    /deep/ .el-form-item {
      margin-bottom: 30px;
      .el-form-item__content  {
        margin-left: 0px
      }
    }
    .tip {
      position: absolute;
      padding: 0 2px;
      left: 18px;
      top: 12px;
      font-size: 16px;
      line-height: 1;
      color: #898989;
      pointer-events: none;
      transition: all .1s linear;
      &::before {
        content: attr(alt);
      }
      &.top::before {
        content: attr(placeholder);
      }
    }
  }
</style>
