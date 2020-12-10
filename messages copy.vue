<template>
    <div>
      <ul>
        <li v-for="(user, index) in this.$store.state.users" :key="index">
        <router-link v-bind:to="'/message/' + user ">
        <div v:bind:id="1">{{user}}</div>
      </router-link>
        </li>
      </ul>
   </div>

</template>

<script>
export default {
  data() {
    return {
      dataHistory: [],
      users: this.$store.state.users,
      id: ""
    };
  },
  methods: {},
  created() {
  
  var myHeaders = new Headers();
myHeaders.append("Authorization",this.$store.state.data.token);
myHeaders.append("Content-Type", "application/json");


var raw = JSON.stringify({ "login":this.$store.state.data.login
                          
                          });



  var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};
 
     fetch("http://localhost:8080/users", requestOptions)
     .then(res => res.json())
    .then(json => this.$store.state.users = json)
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
  border-collapse: collapse;
  max-width: 80%;
  margin : 0 auto;
}

th, td {
  text-align: left;
  padding: 8px;
}

tr:nth-child(even){background-color: #f2f2f2}

th {
  background-color: #4CAF50;
  color: white;
}

.headerTable{
    font-family: Lato-Bold;
    font-size: 15px;
    color: #00ad5f;
    line-height: 1.4;
    text-transform: uppercase;
    background-color: #393939;

}

.lineTable{
font-family: Lato-Regular;
font-size: 15px;
color: #808080;
line-height: 1.4;
background-color: #222222;
};
</style>