<template>
  <el-aside class="leftmenu">
    <div class="waptool" @click.prevent="wapleftmenucollapse"><i class="el-icon-menu"></i></div>
    <el-scrollbar class="hiddenX" style="height:100%">
      <transition name="fadein">
        <div v-show="wapisCollapse">
          <el-menu  :default-active="$route.path" :default-openeds="openeds" background-color="transparent" text-color="#333" @open="handleOpen" @close="handleClose" :collapse="isCollapse" unique-opened mode="vertical" router>
              <el-row class="leftmenutoolbox">
                <div @click.prevent="leftmenucollapse" class="tools"><i class="el-icon-menu"></i></div>
              </el-row>
              <template v-for="(leftmenu,index) in $router.options.routes">
                <el-submenu :index="leftmenu.path" v-if="leftmenu.children">
                    <template slot="title"><i :class="leftmenu.icon"></i><span slot="title">{{leftmenu.name}}</span></template>
                    <el-menu-item v-for="leftmenuchild in leftmenu.children" :index="leftmenuchild.path" :key="leftmenuchild.path"><i :class="leftmenuchild.icon"></i>{{leftmenuchild.name}}</el-menu-item>
                </el-submenu>
                <!-- <el-menu-item v-if="!leftmenu.children" :index="leftmenu.path"><i :class="leftmenu.icon"></i><span slot="title">{{leftmenu.name}}</span></el-menu-item> -->
              </template>
          </el-menu>
        </div>
      </transition>
    </el-scrollbar>
  </el-aside>
</template>

<script>
export default {
  name: 'LeftMenu',
  data: function () {
    return {
      openeds: ['/kszl/'],
      activeIndex: '',
      isCollapse: false,
      wapisCollapse: true
    }
  },
  created: function(e){
    if(window.innerWidth < 900){
      this.wapisCollapse = false
    }
  },
  methods: {
    handpp: function(pp){
      console.log(pp)
    },
    handleOpen(key, keyPath) {
      //console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      //console.log(key, keyPath);
    },
    leftmenucollapse:function(){
      this.isCollapse = !this.isCollapse
    },
    wapleftmenucollapse:function(){
      this.wapisCollapse = !this.wapisCollapse
    }
  },
}
</script>

<style lang="scss" scoped>
@import "common/scss/index.scss";

.leftmenu{ width:auto !important; display: flex; background: $color-background-white; }
.leftmenu .el-menu:not(.el-menu--collapse) { width: 200px; flex: 0 0 200px; }
.leftmenu .el-menu .el-menu-item.is-active{ background-color: $color-theme !important; color: #fff !important; }
.leftmenutoolbox{ width: 100%; display: block; padding: 0px 0px; }
.leftmenutoolbox .tools{ width: 60px; height: 60px; font-size: 20px; text-align: center; line-height: 60px; color: #333; }

</style>
