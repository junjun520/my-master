<template>
  <el-row>
    <el-col :span="24"><div class="grid-content bg-purple-dark">{{msg}}</div></el-col>
  </el-row>
</template>

<script>
  export default {
    data() {
      return {
        msg: 'Tourism'
      }
    }
  }
</script>

<style lang="scss">
  .bg-purple-dark {
    color: green;
  }
</style>
