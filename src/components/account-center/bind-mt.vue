<template>
  <article class="popup modify-mt" v-show="show">
    <div class="popup-main">
      <header>
        绑定MT账号
        <i class="close" @click="close">×</i>
      </header>
      <div class="popup-content">
        <el-form ref="form" :model="form" label-width="100px">
          <el-form-item label="MT账号">
            <el-input v-model="form.id" :disabled=true></el-input>
          </el-form-item>
          <el-form-item label="密码">
            <el-input type="password" v-model="form.pas" placeholder="请输入新的MT账号交易密码"></el-input>
          </el-form-item>
          <el-form-item label="交易杠杆">
            <el-select v-model="form.leverage" placeholder="请选择交易杠杆">
              <el-option  v-for="item in leverageList" :key="item" :label="item" :value="item"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="验证码" class="verify-input">
            <el-input v-model="form.verify" placeholder="请输入右侧验证码"></el-input>
            <div class="verify-img">
              <img src="../../assets/img/logo.png"/>
            </div>
          </el-form-item>
        </el-form>
        <div class="popup-btns">
          <button class="hot-bg" @click="close">取消</button>
          <button class="cold-bg" @click="addMt">添加</button>
        </div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  name: 'bind-mt',
  data () {
    return {
      form: {
        id: 123,
        pas: '',
        leverage: '',
        verify: ''
      },
      leverageList: [
        '1:100',
        '1:200',
        '1:300',
        '1:400'
      ]
    };
  },
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  computed: {
  },
  created: function () {
  },
  methods: {
    close () {
      for (let item in this.form) {
        this.form[item] = '';
      }
      this.$emit('update:show', false);
    },
    addMt () {
      if (this.form.pas === '') {
        this.$message({
          type: 'success',
          message: '内容不许为空！'
        });
      } else {
        let mt = {
          id: this.form.id,
          pas: this.form.pas,
          leverage: this.form.leverage,
          mainAccount: false,
          status: true
        };
        this.$store.commit('addMtList', mt);
        this.$message({
          type: 'success',
          message: '添加成功!'
        });
        this.close();
      }
    }
  }
};
</script>

<style lang="less" scoped>
  .modify-mt{
    .verify-input{
      text-align: left;
      .el-input{
        width: 60%;
        margin-right: 5%;
      }
      .verify-img{
        display: inline-block;
        width: 24%;
        height: auto;
      }
    }
  }
</style>
