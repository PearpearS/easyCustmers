<template>
  <div class="add container">
    <h1 class="page-header">添加用户</h1>
    <form v-on:submit="addCustomer">
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
            <button type="submit" class="btn btn-info">添加</button>
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
      addCustomer(e){
          if(!this.customer.name||!this.customer.phone||!this.customer.email){
              console.log("meitian");
          }else{
              let newCustomer={
                  name:this.customer.name,
                  phone:this.customer.phone,
                  email:this.customer.email,
                  education:this.customer.education,
                  school:this.customer.school,
                  work:this.customer.work,
                  profile:this.customerprofile
              }
              this.$http.post("http://localhost:3000/user",newCustomer)
                  .then((responese)=>{
                      console.log(responese);
                      this.$router.push({path:'/',query:{alert:`添加${newCustomer.name}用户成功`}});
                  })
          }
          e.preventDefault();
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
