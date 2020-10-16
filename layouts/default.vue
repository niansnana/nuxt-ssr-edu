<template>
  <el-container>
    <!-- 侧边栏 -->
    <Aside :get-collapse="collapse" :is-hidden="isHidden" />
    <!-- 抽屉侧边栏 -->
    <el-drawer :visible.sync="drawer" :direction="direction" :show-close="false">
      <!-- <el-aside>
        <el-menu
          class="el-menu-vertical-demo"
          :collapse="collapse"
          :default-active="slideMenuActive"
        >
          <nuxt-link to="/">
            <el-menu-item index="/">
              <i class="el-icon-s-home"></i>
              <span slot="title">首页</span>
            </el-menu-item>
          </nuxt-link>
          <el-submenu v-for="item in slideMenu" :key="item.id" :index="item.path">
            <template slot="title">
              <i :class="item.icon"></i>
              <span slot="title">{{item.title}}</span>
            </template>
            <nuxt-link v-for="subItem in item.children" :key="subItem.id" :to="subItem.path">
              <el-menu-item
                :index="subItem.path"
                @click="handleSelect(subItem.path)"
              >{{subItem.title}}</el-menu-item>
            </nuxt-link>
          </el-submenu>
        </el-menu>
      </el-aside>-->
      <Aside :get-collapse="collapse" :is-hidden="!isHidden" @get-drawer="getDrawer" />
    </el-drawer>
    <!-- 主区域 -->
    <el-container>
      <!-- 头部区 -->
      <el-header>
        <el-row :gutter="20">
          <el-col :lg="1" :md="1">
            <el-button class="hidden-md-and-down" :icon="isCollapse" @click="toggleCollapse"></el-button>
            <el-button
              class="hidden-md-and-up"
              icon="el-icon-s-operation"
              type="primary"
              style="margin-left: 16px;"
              @click="drawer = true"
            ></el-button>
          </el-col>
          <el-col :lg="4" :md="2">
            <el-input
              v-model="searchValue"
              placeholder="搜索学员姓名/班级名称"
              class="input-with-select"
              clearable
            >
              <i slot="suffix" class="el-icon-search el-input__icon"></i>
            </el-input>
          </el-col>
          <el-col :lg="6" :md="1" :offset="13">
            <i class="el-icon-edit"></i>
            <i class="el-icon-share"></i>
            <i class="el-icon-delete"></i>
          </el-col>
        </el-row>
      </el-header>
      <!-- 内容展示 -->
      <el-main>
        <Nuxt />
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import Aside from '@/components/aside/index'
export default {
  components: { Aside },
  data() {
    return {
      collapse: false, // 侧边栏是否打开，默认展开
      drawer: false, // 默认不展示抽屉视窗
      direction: 'ltr', // 左侧打开
      isHidden: false,
      searchValue: ''
    }
  },
  computed: {
    isCollapse() {
      return this.collapse ? 'el-icon-s-unfold' : 'el-icon-s-fold'
    },
    setHeaderAutoChange() {
      return 0
    }
  },
  methods: {
    toggleCollapse() {
      this.collapse = !this.collapse
    },
    getDrawer(value) {
      this.drawer = value
    }
  }
}
</script>

<style lang="stylus" scoped>
.el-container
  height 100%
  .el-aside
    background-color #fff
</style>
