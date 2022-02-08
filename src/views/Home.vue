<template>
  <div class="container">
    <div class="form-container">
      <form @submit.prevent="submitLogin" class="form">
        <div>
          <label for="username">Username</label>
          <div class="space"></div>
          <input v-model="form.username" type="text" placeholder="Enter your username">
          <p class="error" v-if="errors.username">The username is incorrect.</p>
          <p class="error" v-if="counterrors.username">The username cannot be less than 5 characters</p>

        </div>
        
        <div class="mtop">
          <label for="password">Password</label>
          <div class="space"></div>
          <input type="password" v-model="form.password" placeholder="Min. 8 characters">
          
          <p class="password-error" v-if="errors.password" >The password is incorrect.</p>
          <p class="password-error" v-if="counterrors.password" >The password cannot be less than 10 characters</p>

        </div>

        <button type="submit">Login</button>

        <!-- <div v-if="form.username" style="color:black; border:2px solid #444444; background: #eeeeee; font-size:1.3em; padding:20px;">
          {{form.username}}
        </div> -->

      </form>


      <!-- <div class="options">
        <form action="" class="span">
          <input type="checkbox" name="Remeber Me?" id="RemeberMe" class="checkbox">
          <label for="RememberMe" class="label">Remeber Me</label>
        </form>

        <a href="#">Forgot Password?</a>

      </div> -->

    </div>
  </div>
</template>

<script>

export default {

  data() {
    return {

      errors: {
        username: false,
        password: false
      },

      counterrors: {
        username: false,
        password: false
      },

      form: {
        username: '',
        password: '',
      },

      user_from_db: {
        usernameInput: "Qaudri",
        passwordInput: "Qaudri1234",
      },
    }
    
  },

  methods: { 

    validateInput(){
      if(this.form.username < 5){
        this.counterrors.username = true
        // console.log(this.errors)
       
        if(this.form.password < 10){
          this.counterrors.password = true
          // console.log(this.errors)
        }
        
        else {
          this.counterrors.password = false
        }

      }else{

        this.counterrors.username = false
      }
    },

    submitLogin(){

      this.validateInput()

      if (this.form.username == this.user_from_db.usernameInput) {
        
        if (this.form.password == this.user_from_db.passwordInput) {
          this.$router.push("/dashboard")
        } else {
          this.errors.password = true
          return
        }
      } else {
        this.errors.username = true
        return
      }
    
    }, 
  }
}
</script>

<style>
.container{
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-items: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
}

.form-container{
  background: #eeeeee;
  border: 1px solid #a8a8a8;
  border-radius: 10px;
  padding: 20px;
  margin: auto;
  width: 20vw;

}

.form{
  margin-top: 20px;
}

.form label{
  font-size: 1rem;
  font-weight: 500;
}

.space{
  padding: 5px 0px;
}

.form input{
  width: 100%;
  border: none;
  outline: none;
  padding: 10px 0px 10px 10px;
  border-radius: 5px;
}

.options{
  display: flex;
  justify-content: space-between;
  margin: 10px 0px;
}

.label{
  font-size: .8rem;
  color: #a8a8a8;
}

.span{
  display: flex;
  align-items: center;
}

a{
  text-decoration: none;
  color: #a8a8a8;
  font-size: .8rem;
  font-weight: 500;
}

.mtop{
  margin-top: 20px;
}

button{
  width: 100%;
  border-radius: 5px;
  text-align: center;
  padding: 10px 0px;
  outline: none;
  border: none;
  background: #cccccc;
  color: black;
  font-weight: 600;
  font-size: 1rem;
  margin-top: 15px;
}

button:hover{
  border: 1px solid black;
}

.error{
  font-size: .8rem;
  margin: 5px 0px;
  color: #b32929;
}

.password-error{
  font-size: .8rem;
  margin: 5px 0px;
  color: #b32929;
}

</style>
