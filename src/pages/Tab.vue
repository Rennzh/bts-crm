<template>
  <div class="tab">
    <recharge :show.sync="showRecharge"></recharge>
    <mention :show.sync="showMention"></mention>
    <header class="tab-head is-flex">
      <h1>
        <img src="../assets/img/logo.png" :alt="DeployApi.SystemName">
      </h1>
      <h2>{{DeployApi.SystemName}}</h2>
      <nav class="is-flex">
        <ul class="is-flex nav-actions">
          <li v-for="item in navList" :key="item.icon" @click="userAction(item.index)">
            <i class="iconfont" :class="item.icon"></i>
          </li>
        </ul>
        <div class="user-menu top-nav-submenu">
          <!-- <el-dropdown @command="userAction">
          <span class="el-dropdown-link">
            <img src="../assets/img/user.jpg" />
            {{user.name}}
            <i class="el-icon-caret-bottom el-icon--right"></i>
          </span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item command="userCenter">个人信息</el-dropdown-item>
              <el-dropdown-item command="book">切换Book</el-dropdown-item>
              <el-dropdown-item command="changePas">修改密码</el-dropdown-item>
              <el-dropdown-item command="exit">退出</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown> -->
          <!-- <span class="">
            <img src="../assets/img/user.jpg" />
            {{user.name}}
            <i class="el-icon-caret-bottom el-icon--right"></i>
          </span> -->
          <el-menu ref="topNav" theme="dark" mode="horizontal" @select="userAction">
            <el-submenu index="top">
              <template class="title" slot="title">
                <img src="../assets/img/user.jpg" />
                {{user.name}}
              </template>
              <el-menu-item index="userCenter">
                个人信息
              </el-menu-item>
              <el-menu-item index="book">
                切换Book
              </el-menu-item>
              <el-menu-item index="changePas">
                修改密码
              </el-menu-item>
              <el-menu-item index="exit">
               退出
              </el-menu-item>
            </el-submenu>
          </el-menu>
        </div>
      </nav>
    </header>
    <div class="tab-main">
      <div class="tab-nav">
        <el-menu :default-active="defaultRoute" class="el-menu-vertical-demo" @select="goRouter">
          <el-menu-item v-for="item in navLeftList" :key="item.index" :index="item.index">
            <i class="iconfont" :class="item.icon"></i>
            {{item.text}}
          </el-menu-item>
        </el-menu>
      </div>
      <div class="tab-content">
        <keep-alive>
          <router-view></router-view>
        </keep-alive>
      </div>
    </div>
  </div>
</template>

<script>
import recharge from '@comps/recharge.vue';
import mention from '@comps/mention.vue';
import { mapGetters } from 'vuex';
export default {
  name: 'Tab',
  components: {
    recharge,
    mention
  },
  data () {
    return {
      defaultRoute: 'index',
      navList: [
        {
          icon: 'icon-chongzhi',
          index: 'recharge'
        },
        {
          icon: 'icon-tixian',
          index: 'mention'
        }
      ],
      navLeftList: [
        {
          index: 'index',
          icon: 'icon-shouye',
          text: '首页'
        },
        {
          index: 'analysis-transaction',
          icon: 'icon-jiaoyifenxi',
          text: '交易记录'
        },
        // {
        //   index: 'fund-management',
        //   icon: 'icon-churujinguanli',
        //   text: '资金管理'
        // },
        {
          index: 'money-records',
          icon: 'icon-churujinguanli',
          text: '出入金记录'
        },
        {
          index: 'capital-flow',
          icon: 'icon-churujinguanli',
          text: '资金流水'
        },
        {
          index: 'report',
          icon: 'icon-baobiao',
          text: '报表'
        },
        {
          index: 'test',
          icon: 'icon-baobiao',
          text: '公共样式'
        }
      ],
      showRecharge: false,
      showMention: false
    };
  },
  computed: {
    ...mapGetters(['user'])
  },
  created: function () {
  },
  methods: {
    userAction (command) {
      switch (command) {
        case 'recharge' :
          this.showRecharge = true;
          break;
        case 'mention' :
          this.showMention = true;
          break;
        case 'userCenter' :
          this.defaultRoute = '';
          this.$router.push('/tab/account-center');
          break;
        case 'book' :
          alert('暂未开发');
          break;
        case 'changePas' :
          alert('暂未开发');
          break;
        case 'exit' :
          alert('暂未开发');
          break;
      }
    },
    goRouter (index) {
      this.$router.push('/tab/' + index);
    }
  }
};
</script>

<style lang="less" scoped>
@top-nav-submenu-bg: #353943;
@top-nav-submenu-active-bg: #282b34;
@active-color: #52e3ff;
.tab {
  width: 100%;
  height: 100%;
  position: relative;
  .tab-head{
    width: 100%;
    height: 60px;
    line-height: 60px;
    border-bottom: 1px solid #000;
    position: relative;
    color:#94959a;
    background:#23262d;
    box-sizing: border-box;
    h1{
      width: 60px;
      margin: 0 20px;
      height: auto;
    }
    h2{
      height: 100%;
      font-size:18px;
      font-weight: 600;
      color:#00a4ca;
    }
    nav{
      position: absolute;
      width: auto;
      height: 60px;
      line-height: 60px;
      right: 30px;
      top: 0;
      color: #94959a;
      ul{
        flex: 1;
        justify-content: space-around;
        li{
          // margin-right: 40px;
          // width: 25px;
          // width: 100%;
          height: auto;
          i{
            font-size: 25px;
          }
        }
      }
      .user-menu{
        width: auto;
        height: 60px;
        display: flex;
        img{
          width: 45px;
          height: 45px;
          border-radius: 50%;
        }
        .icon{
          width: 30px;
          height: 30px;
        }
        .el-dropdown{
          width: auto;
          height: 60px;
          line-height: 60px;
          color: #94959a;
          text-align: left;
          font-size: 16px;
          i{
            font-size: 12px;
          }
        }
      }
    }
  }
  .tab-main{
    width: 100%;
    height: calc(~"100% - 60px");
    display: flex;
    .tab-nav{
      width: 100px;
      height: 100%;
      background:#30333c;
      .el-menu{
        background:#30333c;
        font-size:14px;
        line-height:14px;
      }
      .el-menu-item{
        color:#5e718d;
        height: 100px;
        text-align: center;
        line-height: 20px;
        overflow: hidden;
        i{
          display: block;
          width: 100%;
          height: 30px;
          line-height: 30px;
          font-size: 30px;
          margin-top: 25px;
        }
      }
      .el-menu-item:nth-of-type(1){
        text-indent: 0;
      }
      .el-menu-item:hover{
        color:#52e3ff;
        background:#30333c;
      }
      .el-menu--horizontal.el-menu--dark .el-submenu .el-menu-item.is-active, .el-menu-item.is-active{
        color: #52e3ff;
        background: #26282f;
      }
    }
    .tab-content{
      flex: 1;
      background: #212227;
      box-shadow: inset 4px 2px 4px 0 rgba(0,0,0,0.50);
      height: 100%;
      overflow: auto;
    }
  }
}
.nav-actions {
  li {
    margin-right: 40px;
  }
}
</style>
