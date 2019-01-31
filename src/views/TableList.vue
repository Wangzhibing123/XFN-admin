<template>
  <div class="">
    <el-breadcrumb separator="/">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>桌台管理 </el-breadcrumb-item>
      <el-breadcrumb-item>桌台列表</el-breadcrumb-item>
    </el-breadcrumb>
    <el-row>
      <el-col :xs="12" :sm="8" :md="6" :lg="4" xl="2" v-for="(n,index) in 48" :key="index">
        <xfn-table></xfn-table>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import Table from '../components/Table'
export default {
  components:{
    'xfn-table':Table
  }
}
</script>