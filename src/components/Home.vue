<template>
  <div class="container">
    <h1>{{msg}}</h1>
    <el-row :gutter="24">
      <el-col :span="8" :offset="9">
        <el-input v-model="name" placeholder="姓名"></el-input>
        <el-input v-model="age" placeholder="年龄"></el-input>
        <el-button type="primary" @click="addUser()">提交</el-button>
      </el-col>
    </el-row>
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
      }
    },
    methods : {
      addUser(){
        
        var postdata = {
          name : this.name,
          age : this.age
        };
        
        axios.post('http://127.0.0.1:9090/setdata',qs.stringify(postdata))
          .then(function(res){
            console.log(res.data);
            alert('提交成功')
          }).catch(function(err){
            console.log(err)
          })
        
        
        // get 请求获取数据
        // axios.get('http://127.0.0.1:9090/getdata')
        //  .then((res)=>{
        //     var data = res.data;
        //     console.log(data)
        //     this.name = data[0].name;
        //     this.age = data[0].age
        //  });
      }
    }
  }
</script>

<style>
  .el-input{ width: 30%; float: left; margin-right: 10px}
  button{ float: left; }
</style>