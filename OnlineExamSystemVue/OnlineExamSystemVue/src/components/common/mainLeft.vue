<!--左边下拉导航栏-->
<template>
  <div id="left">
    <el-menu active-text-color="#000" text-color="#000" :default-active="this.$route.path" class="el-menu-vertical-demo"
      @open="handleOpen" @close="handleClose" :collapse="flag" background-color="#fff" menu-trigger="click" router>
      <el-submenu v-for="(item, index) in menu" :index='item.index' :key="index">
        <template slot="title">
          <div class="left-width">
            <i class="iconfont" :class="item.icon" style="font-size: 22px;"></i>
            <span slot="title" class="title">{{ item.title }}</span>
          </div>
        </template>
        <el-menu-item-group v-for="(list, index1) in item.content" :key="index1">
          <el-menu-item @click="handleTitle(item.index)" :index="list.path" v-if="list.item1 != null"
            style="color:white;"><i :class="list.icon" style="font-size: 20px;color: white;">
            </i>{{ list.item1 }}</el-menu-item>
          <el-menu-item @click="handleTitle(item.index)" :index="list.path" v-if="list.item2 != null"
            style="color:white;"><i :class="list.icon" style="font-size: 20px;color: white;">
            </i>{{ list.item2 }}</el-menu-item>
          <el-menu-item @click="handleTitle(item.index)" :index="list.path" v-if="list.item3 != null"
            style="color:white;"><i :class="list.icon" style="font-size: 20px;color: white;">
            </i>{{ list.item3 }}</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
    </el-menu>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: "mainLeft",
  data ()
  {
    return {

    }
  },
  computed: mapState(["flag", "menu"]),
  created ()
  {
    this.addData()
  },
  methods: {
    handleOpen (key, keyPath)
    {
      // console.log(key, keyPath);
    },
    handleClose (key, keyPath)
    {
      // console.log(key, keyPath);
    },
    //点击标题传递参数给navigator组件
    handleTitle (index)
    {
      this.bus.$emit('sendIndex', index)
    },
    addData ()
    {
      let role = this.$cookies.get("role")
      if (role == 0) {
        this.menu.push({
          index: '5',
          title: '教师管理',
          icon: 'el-icon-a-05',
          content: [{ item1: '教师管理', path: '/teacherManage', icon: "el-icon-a-041" }, { item2: '添加教师', path: '/addTeacher', icon: "el-icon-a-07" }],
        })
      }
    }
  },
}
</script>

<style>
.el-menu-vertical-demo .el-submenu__title {
  color: #000;
  overflow: hidden;
}

.left-width .iconfont {
  font-size: 18px;
  color: #fff;
}

.left-width {
  width: 213px;
}

.el-menu-vertical-demo:not(.el-menu--collapse) {
  min-height: 900px;
}

#left {
  height: 900px;
  background-color: #fa6286;
  z-index: 0;
}

#left .el-menu-vertical-demo .title {
  color: #000;
  font-size: 16px;
  font-weight: bold;
  margin-left: 14px;
}

.el-submenu {
  color: #000;
}

.el-submenu__title:hover {
  color: #000;
  background-color: #000;
}

/* .el-submenu__title i {
  color: #000 !important;
} */

.el-menu-item {
  color: #000 !important;
}

.el-menu-item i {
  color: #000 !important;
}
</style>
