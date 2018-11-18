<template>
  <div class="detail container">
   <router-link to='/' class="btn btn-default">返回</router-link>
   <h1 class="page-header">{{customers.name}}
       <span class="pull-right">
           <router-link class="btn btn-primary" v-bind:to="'/edit/'+customers.id">
                编辑
            </router-link>
            <button class="btn btn-danger" v-on:click="deleteUser(customers.id)">删除</button>
       </span>
   </h1>
   <ul class="list-group">
       <li class="list-group-item"><span class="glyphicon glyphicon-earphone">{{customers.phone}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon-envelope">{{customers.email}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon-education">{{customers.education}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon-bookmark">{{customers.school}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon-leaf">{{customers.work}}</span></li>
       <li class="list-group-item"><span class="glyphicon glyphicon-user">{{customers.profile}}</span></li>
   </ul>
   
  </div>
</template>

<script>
export default {
  name: 'detail',
  data () {
    return {
        customers:{}
    }
  },
  methods:{
      fetchCustomers(id){
      this.$http.get("http://localhost:3000/user/"+id)
          .then((response)=>{
            console.log(response);
            this.customers=response.data;
          })
    },
    deleteUser(id){
        this.$http.delete("http://localhost:3000/user/"+id)
            .then((response)=>{
                this.$router.push({path:'/',query:{alert:`删除用户  ${this.customers.name}  成功`}})
            })
    }
},
     created(){
        this.fetchCustomers (this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.glyphicon:before{
    padding-right: 20px!important;
}
</style>
