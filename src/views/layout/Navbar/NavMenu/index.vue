<template>
<div class="nav-menu">
  <div class="user-container" v-if="user.id">
    <div class="write-container" @click="goPath('/editor/drafts/new')">
      <icon-svg icon-class="write"></icon-svg>
      <span class="container-name">写文章</span>
    </div>
    <el-dropdown menu-align="start"
      class="avatar-container"
      trigger="click"
      @visible-change="visibleChange">
      <div class="avatar-wrapper" :class="{'active' : isShowDrop}">
          <span class="wrapper-name">{{ user.name }}</span>
          <span class="wrapper-icon">▼</span>
      </div>
      <el-dropdown-menu class="user-dropdown" slot="dropdown">
          <el-dropdown-item @click.native="goPath('/mySpace')">
              我的空间
          </el-dropdown-item>
          <el-dropdown-item @click.native="goPath('/personalData')">
              个人资料
          </el-dropdown-item>
          <el-dropdown-item @click.native="goPath('/changepsw')">
              密码修改
          </el-dropdown-item>
          <el-dropdown-item @click.native="goPath('/collection')">
              我的收藏
          </el-dropdown-item>
          <el-dropdown-item @click.native="logout">
              退出登录
          </el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
  </div>
  <!-- login bar (if not logined) -->
  <ul v-else class="login-container">
    <li class="login-name"><router-link to="/login/">登录</router-link></li>
    <!-- insert separator -->
    <li class="login-separator">|</li>
    <li class="login-name"><router-link to="/signup/">注册</router-link></li>
  </ul>
</div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  data () {
    return {
      isShowDrop: false
    }
  },
  computed: {
    ...mapGetters(['user'])
  },
  mounted () {
  },
  updated () {
  },
  methods: {
    logout () {
      this.$store.dispatch('Logout').then(() => {
        location.reload() // 为了重新实例化vue-router对象 避免bug
      })
    },
    goPath (path) {
      this.$router.push({path: path})
    },
    visibleChange () {
      this.isShowDrop = !this.isShowDrop
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.login-container {
  color: #ffffff;
  float: right;
  margin-left: 50px;
  .login-name {
    font-size: 16px;
    float: left;
    position: relative;
    cursor: pointer;
    padding: 0px 10px;
    width: 55px;
    &:hover {
    font-weight: bold;
    }
  }
  .login-separator {
    float: left;
    position: relative;
    padding: 0px 5px 0px 2px;
  }
}
.user-container {
  margin-left: 40px;
}
.write-container {
  display: inline-block;
  cursor: pointer;
  color: #fff;
  position: relative;
  cursor: pointer;
  padding: 0px 1px;
  width: 75px;
  .container-name {
    font-size: 16px;
    &:hover {
      font-weight: bold;
    }
  }
}
.avatar-container {
  text-align: center;
  font-size: 18px;
  display: inline-block;
  .avatar-wrapper {
    width: 100px;
    cursor: pointer;
    transition: all 0.5s ease-in-out;
    color: #fff;
    .wrapper-icon {
      font-size: 13px;
    }
    .wrapper-name {
      font-size: 16px;
      max-width: 60px;
      display: inline-block;
      padding: 1px;
      &:hover {
      font-weight: bold;
      }
    }
  }
  .avatar-wrapper.active {
    color: #ffffff;
    box-shadow: inset 0 0 3px 0 rgba(0, 0, 0, 0.09);
    border-radius: 2px 2px 0 0;
    background: #2953fc;
  }
}

// dropdown style
.user-dropdown {
  width: 100px;
  margin-top: 0;
  background-color: #5677fc;
  padding-top: 0;
  margin-top: 1px;
  border-radius: 0 0 4px 4px;
  border: 0;
  /deep/ .popper__arrow {
    display: none;
  }
  /deep/ .el-dropdown-menu__item {
    padding: 10px 15px;
    transition: all 0.3s ease-in-out;
    line-height: normal;
    font-size: 13px;
    color: #ffffff;
    text-align: center;
    &:hover {
      background-color: #2953fc;
    }
    &:active {
      font-weight: bold;
    }
  }
}
</style>
