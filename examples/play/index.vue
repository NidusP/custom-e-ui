<template>
  <div style="margin: 20px; padding: 50px; display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap; background-color: olivedrab">
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

    <el-select v-model="select" custom multiple prefix-label="多选">
      <el-option v-for="(item, index) in option" :key="index" :label="item.value" :value="item.value"></el-option>
    </el-select>

    <div class="" style="font-size: 20px">
      <el-select v-model="input" custom prefix-label="关键词1" :popper-append-to-body="false" clearable>
        <el-option v-for="(item, index) in option" :key="index" :label="item.value" :value="item.value"></el-option>
      </el-select>
    </div>

    <div style="background-color: darkseagreen; color: black" v-loading.custom="locationState"
         element-loading-text="loading"
         element-loading-spinner="el-icon-loading"
         element-loading-customClass="loading-blur"
         element-loading-background="rgba(0, 0, 0, 0)">测试自定义指令loading</div>
    <div class="block">
      <span class="demonstration">带快捷选项</span>

      <el-date-picker
              custom
              v-model="value2"
              type="daterange"
              align="right"
              unlink-panels
              range-separator="至"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
              :picker-options="pickerOptions">
      </el-date-picker>
    </div>

    <el-table
            :data="tableData"
            style="width: 100%"
            border
            :row-class-name="tableRowClassName">
      <el-table-column
              prop="date"
              label="日期"
              width="180">
      </el-table-column>
      <el-table-column
        label="信息"
      >
        <el-table-column
                prop="name"
                label="姓名"
                width="180">
        </el-table-column>
        <el-table-column
                prop="address"
                label="地址">
        </el-table-column>
      </el-table-column>
    </el-table>

    <el-button type="text" @click="dialogVisible = true">点击打开 Dialog</el-button>

    <el-dialog
            :visible.sync="dialogVisible"
            width="30%"
            custom-class="model-class"
            append-to-body
    >
      <h4 class="title" slot="title">添加算法</h4>
      <el-select placeholder="请选择" custom  v-model="select">
      </el-select>
    </el-dialog>
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
        dialogVisible: false,
        locationState: true,
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
        optionEmpty: [],
        pickerOptions: {
          shortcuts: [{
            text: '最近一周',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit('pick', [start, end]);
            }
          }, {
            text: '最近一个月',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              picker.$emit('pick', [start, end]);
            }
          }, {
            text: '最近三个月',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
              picker.$emit('pick', [start, end]);
            }
          }]
        },
        value2: '',
        tableData: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }]
      };
    },
    methods: {
      handleClose(done) {
        this.$confirm('确认关闭？')
                .then(_ => {
                  done();
                })
                .catch(_ => {});
      },
      tableRowClassName({row, rowIndex}) {
        if (rowIndex === 1) {
          return 'warning-row';
        } else if (rowIndex === 3) {
          return 'success-row';
        }
        return '';
      }
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
  /deep/.el-table .warning-row {
    background: #ffd069;
  }

  /deep/.el-table .success-row {
    background: #96f98a;
  }
</style>
