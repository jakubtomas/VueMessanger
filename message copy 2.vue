<template>

<div class="big-box">

      <div class="small-box">
        <ul class="zoznam">
              <li v-for="(user, index) in this.$store.state.users" :key="index">
            <router-link v-bind:to="'/message/' + user " >
            <!-- <div v:bind:id="1" @submit.prevent="refresh"> {{user}}</div> -->
            <button class="userButtons" @click.prevent="updateMessages(user)">{{user}}</button>
          </router-link>
        </li>
        </ul>
      </div>


      <div class="main-box">
        
            <div class="main-container">
                    <div v-for="(message, index) in messages" :key="index">


                            <div v-if="message.from == myLogin"  class="containerr container-left" >
                              
                              <em class="time-left">From {{message.from}}</em>
                              <!-- <img src="/w3images/bandmember.jpg" alt="Avatar" style="width:100%;"> -->
                              <p class="message message-left" >{{message.message}}</p>
                              <span class="time-right">{{message.datetime}}</span>

                            </div>


                          <div v-else  class="containerr   container-right  darker">
                            
                            <em class="time-left" >From {{message.from}}</em>
                            <!-- <img src="/w3images/bandmember.jpg" alt="Avatar" style="width:100%;"> -->
                            <p class="message message-right">{{message.message}}</p>
                            <span class="time-right">{{message.datetime}}</span>

                          </div>

                    </div>


            </div>
      <div>
        <!-- <textarea  maxlength="300" placeholder="write message" ></textarea> -->
        <form  @submit.prevent="sendMessage">
           <input  class="message-form" type="text"  placeholder="write message"  v-model="message" />
            <!-- <button class="button-send-message">Send</button> -->
          <!-- <p class="message">Not registered? <a href="#">Create an account</a></p> -->
    </form>
         
      </div>
         
      </div>
</div>


</template>

<script>
export default {
  data() {
    return {
      user : "user24",
      dataHistory: [],
      id: this.$route.params.id,
      login : this.$route.params.login,
      myLogin : this.$store.state.data.login,
      messages :[],
      message: "",
      error: ""
    };
  },
  methods: {


sendMessage(){
        // this.$store.state.user.address = 'London';
 

     if (this.message == "") {
       this.error = "Error Empty message"
       
       return
     }
            
        var myHeaders = new Headers();
myHeaders.append("Authorization",this.$store.state.data.token);
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
                          "from": this.myLogin,
                          "message":this.message,
                          "to" : this.login
                          });

  var requestOptions = {
    method: 'POST',
    headers: myHeaders,
    body: raw,
    redirect: 'follow'
  };

console.log(this.value);

fetch("http://localhost:8080/message/new", requestOptions)
  .then(res => res.json())
  .then(json => this.$store.state.sendMessage = json)
  .then(result => console.log(result))
  .catch(error => console.log('problem', error));

 
// tie data tam musi dat asi priamo do index vue cez this 
 // window.location.href = 'http://localhost:8081/message/'+ this.login;
   
     // setTimeout(() => {  this.updateMessages(this.login); }, 10);
   // this.updateMessages(this.login);

  this.message ="";
  // setTimeout(() => {  this.updateMessages(this.login); }, 3000);
    },

    updateMessages(nameUser)
    {
      //setTimeout(() => {  console.log("updateMessage"); }, 2000);
     // console.log("refresh function " + nameUser);
        console.log("function nameUser");
        

       this.login = nameUser;
       this.$route.params.login = nameUser;

      
            var myHeaders = new Headers();
      myHeaders.append("Authorization",this.$store.state.data.token);
      //myHeaders.append("Authorization","692d2cc9291d9d65");
      myHeaders.append("Content-Type", "application/json");
      

      var raw = JSON.stringify({ "from":nameUser,
                          "myLogin":this.myLogin
                          //"myLogin":"user24"
                          });

      
        var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
      };

         fetch("http://localhost:8080/messages", requestOptions)
        .then(res => res.json())
        .then(json => this.messages = json)
        .then(result => console.log(result))
        .catch(error => console.log('problem', error));
      
        //this.message ="";
        

        setTimeout(() => {  this.updateMessages(this.login); }, 3000);
    }
   

  
    

  },
  created(){



  var myHeaders = new Headers();
myHeaders.append("Authorization",this.$store.state.data.token);
//myHeaders.append("Authorization","692d2cc9291d9d65");
myHeaders.append("Content-Type", "application/json");


var raw = JSON.stringify({ "from":this.login,
                          "myLogin":this.myLogin
                          //"myLogin":"user24"
                          });



  var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};
 
     fetch("http://localhost:8080/messages", requestOptions)
     .then(res => res.json())
    .then(json => this.messages = json)
    .then(result => console.log(result))
    .catch(error => console.log('problem', error));
  


  setTimeout(() => {  this.updateMessages(this.login); }, 3000);
 }

 
};


</script>

<style  scoped >


.userButtons{
  background-color: #fff;
  border-radius: 2px;
  margin: 5px 2px;
}

.userButtons:hover {
  background-color: #4CAF50; /* Green */
  color: white;
}

.button-send-message{
  width: 50px;
  height: 68px;
  border-radius:10px ;
}
.message-form {
  width: 400px;
  min-height: 50px;
  resize: none;
  border-radius: 8px;
  border: 1px solid #ddd;
  padding: 0.5rem;
  color: #666;
  box-shadow: inset 0 0 0.25rem #ddd;
  background-color: rgb(213, 216, 213) !important;
 margin: 10px 0px 10px 0px;
}

.button:hover {
  background-color: #4CAF50; /* Green */
  color: white;
}
ul {
  list-style-type: none;
 }
.big-box{
  max-width: 80%;
  /* border: 1px solid red ; */
  margin: 0 auto;
   overflow: hidden;
    position: relative;
    width: 100%;
    margin-top: 35px;
}
.zoznam{
/* margin: 0 auto; */

}
.small-box{
  float: left;
  background-color: rgba(0,0,0,0.4) !important;
  color: #ccc;
  min-width: 80px;
  margin: 0 auto;
  list-style: none;
  min-height: 100%;
  border-radius: 10px;

margin-left: -39px;
   position: absolute;
  /* right: 0; */
  top: 0;

/* min-height: 120%; */
}

.message{
  background-color: #aaaaaa;
  border-radius: 10px;
  border: 1px solid black;
}
.message-left{
     
    margin-left: 10px;
    border-radius: 25px;
    background-color: #82ccdd;
    padding: 5px;
    position: relative;
}
.message-right
{
 
    margin-right: 10px;
    border-radius: 25px;
    background-color: #78e08f;
    padding: 5px;
    position: relative;
}
.main-box{
  border-radius: 16px;
  max-width: 553px;
  margin: 0 auto;
  background-color: rgba(0,0,0,0.4) !important;
} 
.containerr {
  
  /* background-color: #f1f1f112; */
  border-radius: 5px;
  padding: 10px;
  margin: 10px 10px;
  max-width: 500px;
  margin : 0 auto;
  min-width: 352px;
}
.main-container {
  max-width: 700px;
  /* background-color: aqua; */
  display: inline-block;
  overflow-y: auto;
  max-height: 500px;
  /* overflow-y:scroll; */
}
.container-left {
  float: inline-start;
}
.container-right {
  float: inline-end;
}
.darker {
  border-color: #ccc;
  background-color: rgb(128, 119, 1 19);
}

.container::after {
  content: "";
  clear: both;
  display: table;
}

.container img {
  float: left;
  max-width: 60px;
  width: 100%;
  margin-right: 20px;
  border-radius: 50%;
}

.container img.right {
  float: right;
  margin-left: 20px;
  margin-right:0;
}

.time-right {
  float: right;
  /* color: #aaa; */
  margin-bottom: -10px;
  font-size: 10px;
  margin-top: -7px;
  color: white;
}

.time-left {
  color: rgba(255,255,255,0.5);
    font-size: 10px;
  float: left;
  color: #999;
  margin-bottom: -10px;
  color: white;
}
</style>