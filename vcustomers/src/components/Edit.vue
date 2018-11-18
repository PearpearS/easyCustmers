<template>
  <div class="edit container">
    <h1 class="page-header">编辑用户</h1>
    <form v-on:submit="update">
        <div class="well">
            <h4>用户信息</h4>
            <div class="form-group">
                <label>姓名</label>
                <input type="text" class="form-control" placeholder="name" v-model="customer.name" >
            </div>
            <div class="form-group">
                <label>电话</label>
                <input type="text" class="form-control" placeholder="phone" v-model="customer.phone" >
            </div>
            <div class="form-group">
                <label>邮箱</label>
                <input type="text" class="form-control" placeholder="email" v-model="customer.email" >
            </div>
            <div class="form-group">
                <label>学历</label>
                <input type="text" class="form-control" placeholder="education" v-model="customer.education" >
            </div>
            <div class="form-group">
                <label>毕业学校</label>
                <input type="text" class="form-control" placeholder="school" v-model="customer.school" >
            </div>
            <div class="form-group">
                <label>职业</label>
                <input type="text" class="form-control" placeholder="work" v-model="customer.work" >
            </div>
            <div class="form-group">
                <label>个人简介</label>
                <textarea class="form-control" rows="10" v-model="customer.profile"></textarea>
            </div>
            <button type="submit" class="btn btn-info">确认</button>
        </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'add',
  data () {
    return {
        customer:{}
    }
  },
  methods:{
      fetchUser(id){
          //console.log(id);
          this.$http.get("http://localhost:3000/user/"+id)
              .then((response)=>{
                  //console.log(response);
                  this.customer=response.data;
              })
      },
      update(e){
          if(!this.customer.name||!this.customer.phone||!this.customer.email){
              console.log("meitian");
          }else{
              let updateCustomer={
                  name:this.customer.name,
                  phone:this.customer.phone,
                  email:this.customer.email,
                  education:this.customer.education,
                  school:this.customer.school,
                  work:this.customer.work,
                  profile:this.customerprofile
              }
              this.$http.put("http://localhost:3000/user/"+this.$route.params.id,updateCustomer)
                  .then((responese)=>{
                      console.log(responese);
                      this.$router.push({path:'/',query:{alert:`更新用户信息成功`}});
                  })
          }
          e.preventDefault();
      }
  },
  created(){
      this.fetchUser(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
