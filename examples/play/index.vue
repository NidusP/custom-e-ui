<template>
  <div style="margin: 20px; display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap; background-color: olivedrab">
    <el-input v-model="input" placeholder="请输入内容" custom prefix-label="关键词213"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>
    <el-input v-model="input" placeholder="请输入内容"></el-input>

    <el-input v-model="input" custom>
      <template slot="tip">
        <label class="el-input__tip-inner" alt='请输入密码' placeholder='密码'></label>
      </template>
    </el-input>

    <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" class="demo-ruleForm custom-style" :show-message="false">
      <el-form-item  prop="username">
        <el-input name="username" v-model.number="ruleForm.username"  @focus="handleFocus" @blur="handleBlur" placeholder="asd"></el-input>
        <label class="tip" alt='请输入用户名' placeholder='用户名' ref="tips-user"></label>
      </el-form-item>
      <el-form-item prop="password">
        <el-input v-model="ruleForm.password" custom>
          <template slot="tip">
            <label class="el-input__tip-inner" alt='请输入密码' placeholder='密码'></label>
          </template>
        </el-input>
      </el-form-item>
      <el-form-item prop="password">
        <el-input name="password" type="password" v-model="ruleForm.password" autocomplete="off" @keydown.13.native="submitForm" @focus="handleFocus" @blur="handleBlur"></el-input>
        <label class="tip" alt='请输入密码' placeholder='密码' ref="tips-pass"></label>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm" size="mini" :loading="doAjax">登录</el-button>
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
      <el-option v-for="(item, index) in option" :key="index" :label="item.value" :value="item.value"></el-option>
    </el-select>

    <el-select v-model="select" custom  :popper-append-to-body="false" multiple>
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
        ]
      };
    },
    methods: {
      async submitForm() {
        const validateResult = await this.$refs['ruleForm'].validate().catch(err => { console.log(err)})
        if (validateResult){
          this.doAjax = true
          const loginResult = await userLogin({ login: this.ruleForm.username, password: this.ruleForm.password }).catch(err => { console.log(err)})
          if (loginResult && loginResult.code === 200){
            this.userLoginState = true
            saveLocalAuthorization(loginResult.data.accessToken)
            const userInfoResult = await this.setUserInfo(true).catch(err => { console.log(err)})
            if (userInfoResult && userInfoResult.code === 200) {
              this.$message({
                message: '登陆成功，正在进入...',
                duration: '2000',
                type: 'success'
              })
              this.$router.push({ name: 'home' })
            }
          } else {
            this.$message({
              message: loginResult instanceof Error ? '登陆失败!请检查网路。' : '登陆失败!请核对用户名或密码。',
              duration: '1000',
              type: 'error'
            })
          }
          this.doAjax = false
        }
      },
      handleFocus(event){
        let $dom = event.target.name === 'username' ? this.$refs['tips-user'] : this.$refs['tips-pass']
        if(event.target.parentElement.parentElement.parentElement.className.indexOf('is-error') === -1){
          $dom.style.color = '#409EFF'
        } else {
          $dom.style.color = '#F56C6C'
        }
        $dom.style.fontSize = '12px'
        $dom.style.transform = 'translate3d(0px, -20px, 0px)'
        $dom.style.backgroundColor = 'transparent'
        $dom.classList.add('top')
      },
      handleBlur(event){
        let $dom = event.target.name === 'username' ? this.$refs['tips-user'] : this.$refs['tips-pass']
        if (!this.ruleForm[event.target.name].trim()){
          $dom.style.fontSize = '16px'
          $dom.classList.remove('top')
          $dom.style.transform = 'translate3d(0px, 0px, 0px)'
        }
        $dom.style.color = '#C0C4CC'
      }
    }
  };
</script>
<style lang="scss">
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
