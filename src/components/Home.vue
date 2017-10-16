<template>
  <div class="container">
    <h1>{{msg}}</h1>

    <el-row :gutter="24">
      <el-col :span="8" :offset="9">
        <el-input v-model="name" placeholder="姓名"></el-input>
        <el-input v-model="age" placeholder="年龄"></el-input>
        <el-button  @click="addUser()" type="primary">提交</el-button>
      </el-col>
    </el-row>

    <el-table :data="tableData" stripe style="width:50%" v-loading="loading">
      <el-table-column prop="name" label="姓名" width="100%"></el-table-column>
      <el-table-column prop="age" label="年龄" width="100%"></el-table-column>
    </el-table>

   
  </div>
</template>

<script>
  import axios from 'axios'
  import qs from 'qs'

  export default {
    name : 'home',
    data(){
      return {
        msg : 'Test',
        name : '',
        age : '',
        tableData : [],
        loading: false
      }
    },
    methods : {
      // 提交数据
      addUser(){
        var postdata = {
          name : this.name,
          age : this.age
        };
        var that = this;
        axios.post('http://127.0.0.1:9090/setdata',qs.stringify(postdata))
          .then(function(res){
            console.log(res.data);
          }).catch(function(err){
            console.log(err)
          })

        this.loading = true;
        this.name = '';
        this.age = '';

        setTimeout(function(){
          that.$message({
            message: '提交成功',
            type: 'success'
          });
          that.loading = false;
          that.tableData.push(postdata)
        }, 1000)


      }
    },
    created : function(){
      // 获取数据
      axios.get('http://127.0.0.1:9090/getdata')
       .then((res)=>{
          var data = res.data;
          console.log(data)
          this.tableData = data;
       });
    }
  }
</script>

<style>
  .el-input{ width: 30%; float: left; margin-right: 10px}
  button{ float: left; }
  .el-table{  margin: 30px auto;}
  table{ width: 100% !important; }
  table th{ text-align: center !important; }
</style>