<template>
  <div id="films">
   <div v-for="(item, index) in messages" :key="index">
      <p>{{item.from}}</p>
      <p>{{item.to}}</p>
      <p>{{item.message}}</p>
      <p>{{item.datetime}}</p>

   </div>

<h4>toto je data History {{dataHistory}}</h4>

  <table>
    <tr>
      <th>Type </th>
      <th>date </th>
      <th>Login </th>
    </tr>


    <tr v-for="(film, index) in dataHistory" :key="index" >
      <td>{{film.type}}</td>
      <td>{{film.datetime}}</td>
      <td>{{film.login}}</td>
    </tr>
  </table>


<!--  Form start function login @keydown.enter  @submit.prevent -->
<h1>Registration user</h1>
  <form class="add-form" @submit.prevent="addUser">    
    ffname <input type="text" v-model="fname"> <br>
    lname <input type="text" v-model="lname"> <br>
    
    login <br><input type="text" v-model="login"> <br>
    Password <input type="text" v-model="password"> <br>
    <button type="submit">Create New User</button>
  </form>


    <!-- <p v-if="Object.values(characters)"> my data <strong>{{Object.values(characters)[0]}}</strong></p> -->
    <p v-if="characters.error"> my data <strong>{{characters.error}}</strong></p>
<div v-else> 
  <strong> fname {{characters.fname}}</strong>
  <p>l name {{characters.lname}}</p>
  <p>password {{characters.password}}</p>
  <p>login {{characters.login}}</p>
  <p> token {{characters.token}}</p>
</div>

<ul>
  <li v-for="(dude, index) in characters" :key="index">
     {{characters.error}}
     </li>
</ul>

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
      films: [],
      message:"Hello ",
      id: "",
      characters : [],
      dataHistory : [],
      messages : []
    };
  },
  methods: {
    addUser(){
        var myHeaders = new Headers();
        
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({"fname":this.fname,
                          "lname":this.lname,
                          "login":this.login,
                          "password":"password123123"
                          });

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};


fetch("http://localhost:8080/signup", requestOptions)
    // .then(function(response) {
    // console.log(response.status); // returns 200

    // })

  .then(res => res.json())
  .then(json => this.characters = json)
  .then(result => console.log(result))
  .catch(error => console.log('problem', error));

    }
  },
  created() {

  var myHeaders = new Headers();
myHeaders.append("Authorization","212e43780f2a59d6");
myHeaders.append("Content-Type", "application/json");


var raw = JSON.stringify({ "from":"user25",
                          "myLogin":"user24"
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
    // .then((response) => response.json())
    // .then((responseJson) => {
    // console.log(responseJson);

 }
};



</script>


<style >
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

.add-form{
  border: 1px solid black;
  margin: 20px 0px;
  margin-bottom: 30px;
};




.container {
  border: 2px solid #dedede;
  background-color: #f1f1f1;
  border-radius: 5px;
  padding: 10px;
  margin: 10px 0;
}

.darker {
  border-color: #ccc;
  background-color: #ddd;
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
  background-color: #fff;
}

.container img.right {
  float: right;
  margin-left: 20px;
  margin-right:0;
}

.time-right {
  float: right;
  color: #aaa;
}

.time-left {
  float: left;
  color: #999;
}
</style>