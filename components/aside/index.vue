<template>
  <el-aside :class="!isHidden ? 'hidden-sm-and-down' : ''" :width="autoSetSlideWidth">
    <el-menu class="el-menu-vertical-demo" :collapse="getCollapse" :default-active="$route.path">
      <nuxt-link to="/">
        <el-menu-item index="/" @click="closeDrawer">
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
          <el-menu-item :index="subItem.path" @click="closeDrawer">{{subItem.title}}</el-menu-item>
        </nuxt-link>
      </el-submenu>
    </el-menu>
  </el-aside>
</template>

<script>
export default {
  props: {
    getCollapse: { type: Boolean, default: false },
    isHidden: { type: Boolean, default: false }
  },
  data() {
    return {
      slideMenu: [
        { id: '1', path: '/jwzx', title: '教务中心', icon: 'el-icon-s-order', children: [{ id: '1', path: '/educenter', title: '教务列表', show: 'showjwzxo' }, { id: '2', path: '/educenter/add', title: '添加教务' }] },
        { id: '2', path: '/xszx', title: '销售中心', icon: 'el-icon-s-goods', children: [{ id: '1', path: '/salecenter', title: '销售列表' }, { id: '2', path: '/salecenter/add', title: '添加销售' }] }
      ],
      collapse: false, // 侧边栏是否打开，默认展开
      slideMenuActive: '0', // 被激活的侧边按钮
      isShowDrawer: false
    }
  },
  computed: {
    // TODO: 回来写.
    autoSetSlideWidth() {
      return this.getCollapse ? '65px' : !this.isHidden ? '200px' : ''
    }
  },
  methods: {
    // 关闭抽屉
    closeDrawer() {
      this.$emit('get-drawer', this.isShowDrawer)
    },
    setSlideMenuActive() {
      this.slideMenuActive = this.$route.name
    }
  }
}
</script>