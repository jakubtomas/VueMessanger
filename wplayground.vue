<template>

<div class="big-box">
    <div class="small-box">
        <ul class="zoznam">
          <li><a href="">Hello</a></li>
          <li><a href="">Hello</a></li>
          <li><a href="">Hello</a></li>
          <li><a href="">Hello</a></li>
          <li><a href="">Hello</a></li>
          <li><a href="">Hello</a></li>
        </ul>
    </div>
    <div class="main-box">
      
      <div >

        <div class="main-container">

              <div   class="containerr container-left" >
                
                <em class="time-left">From Jakub</em>
                <!-- <img src="/w3images/bandmember.jpg" alt="Avatar" style="width:100%;"> -->
                <p class="message message-left" >message hellow how are you </p>
                <span class="time-right">250564654654</span>

              </div>


              <div class="containerr   container-right  darker">
                
                <em class="time-left">Name Katruin</em>
                <!-- <img src="/w3images/bandmember.jpg" alt="Avatar" style="width:100%;"> -->
                <p class="message message-right"> this is mesassdgaôlkajdflk  </p>
                <span class="time-right">4582354</span>

              </div>


        </div>
      </div>

    </div>
    <!-- chatbox__messages__user-message--ind-message -->
 
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
      messages :[]
    };
  },
  methods: {},
  created() {
 
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
  
 }
};
</script>

<style  scoped >
ul {
  list-style-type: none;
 }
.big-box{
  max-width: 80%;
  border: 1px solid red ;

}
.zoznam{
  margin: 0 auto;

}
.small-box{
  float: left;
  background-color: #fff;
  min-width: 100px;
  margin: 0 auto;
  list-style: none;
  
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
  max-width: 80%;
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