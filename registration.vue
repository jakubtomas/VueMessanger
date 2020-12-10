<template>
  <div  id="films">

<!--  Form start function login @keydown.enter  @submit.prevent -->
    <h2>Create new account</h2>


    <p class="alert-danger" v-if="data.error"> Message from server <strong>{{data.error}}</strong></p>

    <div  v-if="data.login" class="alert-success"> 
      <h3>Account successfully has been created</h3>
      <strong> fname {{data.fname}}</strong>
      <p>lname {{data.lname}}</p>
      <p>login {{data.login}}</p>
  
    </div>


<div class="login-page">
  <div class="form">
    <form class="register-form" @submit.prevent="addUser">
      <input type="text" placeholder="fname" v-model="fname "/>
      <input type="text" placeholder="lname" v-model="lname "/>
      <input type="text" placeholder="login" v-model="login"/>
      <input type="password" placeholder="password" v-model="password"/>
      <button>create</button>
      <p class="message">Already registered? <a href="/signin">Sign In</a></p>
    </form>

  </div>
</div>

  </div>


</template>

<script>
export default {
  data() {
    return {
      fname :"",
      lname :"",
      login :"",
      password : "",
      data : [],
    };
  },
  methods: {
    addUser(){
        var myHeaders = new Headers();

myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({"fname":this.fname,
                          "lname":this.lname,
                          "login":this.login,
                          "password":this.password
                          });

  var requestOptions = {
    method: 'POST',
    headers: myHeaders,
    body: raw,
    redirect: 'follow'
  };


fetch("http://localhost:8080/signup", requestOptions)
  .then(res => res.json())
  .then(json => this.data = json)
  .then(result => console.log(result))
  .catch(error => console.log('problem', error));

    }
  },
  created() {
 }

};


</script>


<style scoped >
.add-form{
  border: 1px solid rgb(218, 16, 16);
  margin: 20px 0px;
  margin-bottom: 30px;
}

.alert-success{
  border: 1px solid black;
    background-color: rgb(75, 157, 236);
    color: #101311;
    /* background-color: #d4edda; */
    border-color: #304635;
    border-radius: 15px;
}

.alert-danger{
  color: #721c24;
    background-color: #bb6168;
    border-color: #ec3d79;
      position: relative;
    padding: .75rem 1.25rem;
    margin-bottom: 1rem;
    border: 1px solid transparent;
    border-radius: .25rem;
}



@import url(https://fonts.googleapis.com/css?family=Roboto:300);

.login-page {
  min-width: 250px;
  padding: 8% 0 0;
  margin: auto;
}
.form {
  position: relative;
  z-index: 1;
  background: #FFFFFF;
  max-width: 360px;
  margin: 0 auto 100px;
  padding: 45px;
  text-align: center;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
}
.form input {
  font-family: "Roboto", sans-serif;
  outline: 0;
  background: #f2f2f2;
  width: 100%;
  border: 0;
  margin: 0 0 15px;
  padding: 15px;
  box-sizing: border-box;
  font-size: 14px;
}
.form button {
  font-family: "Roboto", sans-serif;
  text-transform: uppercase;
  outline: 0;
  background: #4CAF50;
  width: 100%;
  border: 0;
  padding: 15px;
  color: #FFFFFF;
  font-size: 14px;
  -webkit-transition: all 0.3 ease;
  transition: all 0.3 ease;
  cursor: pointer;
}
.form button:hover,.form button:active,.form button:focus {
  background: #43A047;
}
.form .message {
  margin: 15px 0 0;
  color: #b3b3b3;
  font-size: 12px;
}
.form .message a {
  color: #4CAF50;
  text-decoration: none;
}
.form .register-form {
  display: block;
}
.container {
  position: relative;
  z-index: 1;
  max-width: 300px;
  margin: 0 auto;
}
.container:before, .container:after {
  content: "";
  display: block;
  clear: both;
}
.container .info {
  margin: 50px auto;
  text-align: center;
}
.container .info h1 {
  margin: 0 0 15px;
  padding: 0;
  font-size: 36px;
  font-weight: 300;
  color: #1a1a1a;
}
.container .info span {
  color: #4d4d4d;
  font-size: 12px;
}
.container .info span a {
  color: #000000;
  text-decoration: none;
}
.container .info span .fa {
  color: #EF3B3A;
}

</style>