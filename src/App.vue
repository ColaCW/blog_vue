<template>
  <div id="app" v-cloak>
    <el-menu class="menu" :default-active="$route.path" router background-color="#333" text-color="#fff" active-text-color="#ffd04b" mode="horizontal">
      <el-menu-item class="menuItem" index="/">网站首页</el-menu-item>
      <el-submenu index="">
        <template class="menuItem" slot="title">博客分类</template>
        <template v-for="categary in categarys">
          <el-menu-item :key="categary.name" :index="'/blogList/' + categary.name">{{ categary.name }}</el-menu-item>
        </template>
      </el-submenu>
      <el-menu-item class="menuItem" index="/resourceShare">资源分享</el-menu-item>
      <el-menu-item class="menuItem" index="/webIntroduce">网站介绍</el-menu-item>
      <el-menu-item class="menuItem" index="/aboutMe">关于我</el-menu-item>
      <i class="el-icon-search search" @click="isSearch = !isSearch"></i>
    </el-menu>

    <!-- <div class="search-box">
      <el-row>
        <el-col :xs="0" :sm="4" :md="4" :lg="4" :xl="4"><div style="height:1px"></div></el-col>
        <el-col :xs="24" :sm="16" :md="16" :lg="16" :xl="16">
          <el-input v-model="keyWords" placeholder="请输入内容"></el-input>
          <el-button>搜索</el-button>
        </el-col>
        <el-col :xs="0" :sm="4" :md="4" :lg="4" :xl="4"><div style="height:1px"></div></el-col>
      </el-row>
    </div> -->

    <router-view style="padding: 0 10px;"></router-view>

    <div class="footer">
      Design by 刘国强个人博客 吉ICP备18002404号
    </div>
  </div>
</template>

<script>
import { getBlogCategorys } from '@/api/blogFront.js';

export default {
  name: 'App',
  data() {
    return {
      categarys: [], // 博客分类
      keyWords: '',
      isSearch: false // 是否显示搜索输入区
    };
  },
  mounted() {
    this.getBlogCategorys();
  },
  methods: {
    // 加载博客分类
    getBlogCategorys() {
      getBlogCategorys().then(res => {
        if (res.status) {
          this.categarys = res.data;
        }
      });
    }
  }
};
</script>
<style deep>
.menu {
  padding-left: 35%;
  font-size: 20px !important;
}
.footer {
  clear: both;
  position: relative;
  margin-top: 30px;
  width: 100%;
  height: 30px;
  text-align: center;
  z-index: 111;
  color: #333;
}
.menuItem,
.el-submenu__title {
  font-size: 18px;
}
.el-menu--horizontal .el-menu .el-menu-item {
  font-size: 16px;
}
ul,
p {
  margin: 0;
}
.search {
  color: white;
  line-height: 60px;
  outline: none;
  cursor: pointer;
}
.search-box {
  width: 100%;
  background: #ffffff;
}
.search-box el-input {
  width: 150px;
  float: left;
}
.search-box el-button {
  float: left;
}
</style>
