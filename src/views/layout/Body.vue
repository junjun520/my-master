<template>
  <div class="info-content">
    <el-row>
      <el-col :span="4" class="content-left" >
        <div class="grid-content bg-purple">
          <div class="header-info">
            <el-row>
              <p class="person-photo"><img src="../../assets/images/photo.jpeg" alt=""></p>
              <p class="name">XJ Chen</p>
            </el-row>
          </div>
          <div class="slide-nav">
            <el-menu router class="el-menu-vertical-demo" default-active="/home" @open="handleOpen">
              <el-menu-item index="/home"><i class="el-icon-menu"></i>News</el-menu-item>
              <el-submenu v-for="nav in navs" :index="nav.title" :key="nav.title">
                <template slot="title"><i class="el-icon-menu"></i>{{nav.title}}</template>
              <el-menu-item v-for="subnav in nav.subnavs" :index="subnav.router" :key="nav.title">
                {{subnav.title}}
              </el-menu-item>
            </el-submenu>
          </el-menu>
          </div>
        </div>
    </el-col>
    <el-col :span="20" class="content-right">
      <Header :parent-data="{bodyHeight}" user-name="xjchen" v-on:childMsg = "getChildMsg">
        <h3 slot="title" class="fl">{{name}}</h3>
      </Header>
      <div class="grid-content bg-purple-light" :style="{maxHeight: bodyHeight + 'px'}">
        <transition name="router-fade" mode="out-in">
    	  	<router-view></router-view>
      	</transition>
      </div>
    </el-col>
    </el-row>
  </div>
</template>

<script>
  import Header from './Header';

  export default {
    data() {
      return {
        navs: [{
            title: 'Tourism',
            subnavs: [{
              title: 'tourism',
              router: '/tourism'
            }]
          },
          {
            title: 'Work',
            subnavs: [{
              title: 'project',
              router: '/project?page=12'
            }]
          },
          {
            title: 'Collect',
            subnavs: [{
              title: 'movie',
              router: '/movie/2'
            }]
          }
        ],

        bodyHeight: '',
        name: ''
      }
    },

    components: {
      Header
    },

    created: function() {
      this.bodyHeight = window.screen.height - 50;
      //this.$router.push('/home');
    },

    mounted() {

    },

    methods: {
      handleOpen(key, keyPath) {
        console.log(key, keyPath)
      },

      getChildMsg(childData) {
        console.log(childData)
        this.name = this.$store.state.userInfo.name + '  Info';
      }
    },
    //监控路由的变化
    watch: {
      $route(to, form) {
        console.log('watch route')
      }
    }
  }
</script>

<style lang="scss">
  @import '../../assets/css/mixin';
  // 路由动画
  .router-fade-enter-active,
  .router-fade-leave-active {
    transition: opacity .3s;
  }

  .router-fade-enter,
  .router-fade-leave-active {
    opacity: 0;
  }

  .info-content {
    @include minWidth(1520px);
  }

  .content-left {
    position: fixed;
    height: 100%;
    background: $fc;
    padding-right: 0!important;
    @include minWidth(250px);
  }

  .content-right {
    position: absolute;
    right: 0;
    @include minHeight(800px);
    .grid-content {
      overflow-y: auto;
      margin-left: 25px;
      margin-top: 20px;
    }
  }

  .header-info {
    @include wh(100%, 200px);
    background: #333;
    position: relative;
    .el-row {
      margin-right: 0!important;
      @include center;
    }
    .name {
      color: $fc;
      text-align: center;
      margin-top: 20px;
    }
    @at-root {
      .person-photo {
        @include wh(128px, 128px);
        border: 5px solid $fc;
        border-radius: 50%;
        position: relative;
        overflow: hidden;
        background: #88acdb;
        cursor: pointer;
      }
      .person-photo img {
        @include wh(100%, auto);
        @include center;
      }
      .person-photo:hover {
        background: #fff;
        border: 5px solid #88acdb;
        -webkit-box-shadow: 0 0 1.5em #88acdb;
        box-shadow: 0 0 1.5em #88acdb;
        -webkit-animation: rockAnimation 0.5s linear infinite alternate;
        -ms-animation: rockAnimation 0.5s linear infinite alternate;
        -moz-animation: rockAnimation 0.5s linear infinite alternate;
        animation: rockAnimation 0.5s linear infinite alternate;
      }
    }
  }
</style>
