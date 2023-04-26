<template>
  <div class="menu" :class="{ 'small-menu': smallMenu }">
    <MenuItem
      v-for="(item, index) in menuTree"
      :key="index"
      :data="item.children"
      :label="item.label"
      :icon="item.icon"
      :depth="0"
      :smallMenu="smallMenu"
    />
    <i @click="smallMenu = !smallMenu" class="expand material-icons" :class="{ expand: expanded }">arrow_circle_right</i>
    
  </div>
</template>

<script>
import MenuItem from '@/components/template/MenuItem.vue';

export default {
  name: 'recursive-menu',
  data: () => ({
    watch:{
      smallMenu(value){
        if(value){
          this.expanded = this.expanded == true ? true : false;
        }
      }
    },
    expanded: false,
    smallMenu: false,
    menuTree: [
      {
        label: "Home",
        icon: "home",
        children: [
          {
            label: "level 1.1",
            children: [
              {
                label: "level 1.1.1",
                children: [
                  {
                    label: "level 1.1.1.1"
                  }
                ]
              }
            ]
          },
          {
            label: "level 1.2"
          }
        ]
      },
      {
        label: "Dashboard",
        icon: "dashboard",
        children: [
          {
            label: "level 2.1",
          },
          {
            label: "level 2.2"
          },
          {
            label: "level 2.3"
          }
        ]
      },
      {
        label: "Settings",
        icon: "settings"
      }
    ]
  }),
  components: {
    MenuItem
  }
}
</script>

<style lang="scss" scoped>
.menu {
  position: fixed;
  height: 100vh;
  width: 240px;
  left: 0;
  top: 0;
  border-right: 1px solid #ececec;
  transition: all .3s ease;
  overflow: auto;
  background-color: #5CB85C;

  i {
    position: fixed;
    left: 100px;
    font-size: 35px;
    bottom: 15px;
    user-select: none;
    cursor: pointer;
    transition: all .3s ease;
    color: #e2d4d4;
    &.expand {
      transform: rotate(180deg);
    }
    
  }

  &.small-menu {
    overflow: inherit;
    width: 60px;
    padding-top: 50px;
    i {
      left: 20px;
    }
  }
}
</style>