<template>
  <div class="customers container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
   <h1 class="page-header">用户管理系统</h1>
   <input type="text" class="form-control" placeholder="搜索" v-model="filterInput">
   <table class="table table-striped">
     <thead>
      <tr>
        <th>姓名</th>
        <th>电话</th>
        <th>邮箱</th>
        <th></th>
      </tr>
     </thead>

     <tbody>
       <tr v-for="(customer,index) in filterBy(customers,filterInput)" v-bind:key="index">
         <td>{{customer.name}}</td>
         <td>{{customer.phone}}</td>
         <td>{{customer.email}}</td>
         <td><router-link class="btn btn-info" :to="'/detail/'+customer.id">详情</router-link></td>
       </tr>
     </tbody>
   </table>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'customers',
  data () {
    return {
      customers:[],
      alert:'',
      filterInput:''
    }
  },
  components:{Alert},
  methods:{
    filterBy(customers,value){
      return customers.filter((customer)=>{
        return customer.name.match(value)
      })
    },
    fetchCustomers(){
      this.$http.get("http://localhost:3000/user")
          .then((response)=>{
            //console.log(response);
            this.customers=response.data;
          })
    }
  },
  created(){
    if(this.$route.query){
      this.alert=this.$route.query.alert
    }
    this.fetchCustomers();
  },
  updated(){
    this.fetchCustomers();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
td{
  line-height: 34px!important;
}
</style>
