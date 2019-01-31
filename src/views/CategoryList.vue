<template>
  <div>
    <el-breadcrumb separator="/">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>
        <a href="/">菜品类别管理</a>
      </el-breadcrumb-item>
      <el-breadcrumb-item>
        <a href="/">类别列表</a>
      </el-breadcrumb-item>
    </el-breadcrumb>
    <br>
    <el-button type="primary" @click="addCategory">添加新的菜品类别</el-button>
    <br>
    <el-table :data="categoryList" stripe border>
      <el-table-column label="编号" prop="cid"></el-table-column>
      <el-table-column label="名称" prop="cname"></el-table-column>
      <el-table-column label="操作" fixed="right">
        <template slot-scope="{row,$index}">
          <el-button type="success" size="mini" @click="updateCategory(row,$index)" plain>修改</el-button>
          <el-button type="danger" size="mini" @click="deleteCategory(row,$index)" plain>删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      categoryList: []
    };
  },
  methods:{
    deleteCategory(c,i){
      this.$confirm('删除操作补课撤销！','提示',{
        type:'warning'
      }).then(()=>{
        let url = this.$store.state.globalSettings.apiUrl+'/admin/category/'+c.cid;
        this.$axios.delete(url).then((res)=>{
          if(res.data.code==200){
            this.categoryList.splice(i,1);
            this.$message.success('菜品类别删除成功');
          }else{
            this.$message.error('类别删除出错'+res.data.msg);
          }
        }).catch((err)=>{
          console.log(err)
        })
      }).catch(()=>{

      })    
    },
    updateCategory(c,i){
      this.$prompt('请输入您想修改的类别名：','提示',{
        inputValue:c.cname
      }).then(({value})=>{

      }).catch((err)=>{

      })
    },
    addCategory(){
      this.$prompt('请输入新的菜品类别名:','提示',{type:'info'}).then(({value})=>{
        let url = this.$store.state.globalSettings.apiUrl+'/admin/category';
        this.$axios.post(url,{cname:value}).then((res)=>{
          if(res.data.code==200){
            this.$message.success('新的类别添加成功')
            //模型数据中添加新的类别
            this.categoryList.push({cid:res.data.cid,caname:value})
          }else{
            this.$message.error('新的类别添加出错：'+res.data.msg )
          }
        }).catch((err)=>{

        })
      }).catch((err)=>{

      })
    }
  },
  mounted() {
    let url = this.$store.state.globalSettings.apiUrl + "/admin/category";
    this.$axios
      .get(url)
      .then(res => {
        this.categoryList = res.data;
      })
      .catch(err => {
        console.log(err);
      });
  }
};
</script>
<style scoped>
</style>