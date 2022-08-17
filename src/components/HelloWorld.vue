<template>
    <!-- <div>
      <h3>Secret Message</h3>
      <label for="msg">Your Message:</label><br>
      <input type="text" id="msg" name="msg" v-model="msg"><br>
      <label for="duration">Duration in minutes:</label><br>
      <input type="text" id="duration" name="duration" v-model="duration"><br><br>
      <input type="submit" value="Send" v-on:click="click_post">
      <input type="submit" value="Share" v-on:click="click_get">
      <ul>
        <li v-for="user in users" v-bind:key="user.id">Share this link : <br>  {{user.message}}</li>
      </ul>
    </div> -->
    
    <div class="form" >
        <h3>Secret Message</h3>
        <input class="button" type="submit" value="View Message" v-on:click="viewmsg">
        <div id="main">
         <label for="msg">Your Message:</label>
        <input type="text" placeholder="Your Secret Message" id="msg" name="msg" v-model="msg">
        <label for="duration">Duration in minutes:</label>
      <input type="number" placeholder="Duration" id="duration" name="duration" v-model="duration">
        <!-- <li v-for="user in users" v-bind:key="user.id">Share this link : <br>  {{user.message}}</li> -->

         <input class="button" type="submit" value="Send" v-on:click="click_post">
      <input class="button" type="submit" value="Share" v-on:click="click_get">
       </div>
    </div>
</template>

<script >
export default {
// import CryptoJS from "crypto-js";


  data() {
    return {
      msg: '',
      duration: '',
      users: []
    }
  },
  methods: {
    click_post() {
        // hash the name with any algorithm
      fetch('https://secretmessage-16452-default-rtdb.firebaseio.com/Secretmessage.json', {
        method: 'POST',
        headers : {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          message: btoa(this.msg),
          duration: this.duration
        })
      });
      // setTimeout(
      //    mydelete() {
      //       const request = new Request('https://secretmessage-16452-default-rtdb.firebaseio.com/Secretmessage.json', { method: 'DELETE'});
      //       const response = fetch(request);
      //       return response.json();
      //     } this.duration);
    },
    viewmsg(){
        const {hash} = window.location;
      var myhash = window.location;
            alert("Your message is "+ atob(hash.replace('#', '')));
    },
    click_get() {
      const {hash} = window.location;
      var myhash = window.location;
      fetch('https://secretmessage-16452-default-rtdb.firebaseio.com/Secretmessage.json').then((response) => {
        if (response.ok){
          return response.json();
        }
      })
      .then((data) => {
        const results = [];
        for (const id in data) {
          results.push({
            id: id,
            message: myhash+data[id]['message'],
            
          });
          // alert(id)
          document.getElementById("main").innerHTML ='<input type="text" value= ' + myhash+data[id]['message'] + ' v-on:click="click_post" style=" display: block; height: 50px; width: 100%; background-color: yellow; border-radius: 10px; padding: 0 10px; font-size: 17px; font-weight: 300;">'
        }
        this.users = results;
      });
      // alert(data)
    // document.getElementById("main").innerHTML = '<li v-for="user in users" v-bind:key="user.id">Share this link : <br>  ' + {{user.message}} + '</li>';
    setTimeout((mydelete) => {
      var time = this.duration;
      var myduration = parseInt(time);
      var timer = myduration * 60000;
      const request = new Request('https://secretmessage-16452-default-rtdb.firebaseio.com/Secretmessage.json', { method: 'DELETE'});
      const response = fetch(request);
      return response.json();
    }, timer);
      
    },
   
   
  }
};

</script>

<style scoped>
/* div {
  color: orange;
  border-radius: 4px;
  padding: 10px 10px;
  margin-left: 400px;
  margin-right: 400px;
}
input{
  width: 200px;
  border-radius: 20px;
} */


.background{
    width: 430px;
    height: 520px;
    position: absolute;
    transform: translate(-50%,-50%);
    left: 50%;
    top: 50%;
}
.background .shape{
    height: 200px;
    width: 200px;
    position: absolute;
    border-radius: 50%;
}
.shape:first-child{
    background: linear-gradient(
        #1845ad,
        #23a2f6
    );
    left: -80px;
    top: -80px;
}
.shape:last-child{
    background: linear-gradient(
        to right,
        #ff512f,
        #f09819
    );
    right: -30px;
    bottom: -80px;
}
.form{
    height: 720px;
    width: 400px;
    background-color: rgba(255,255,255,0.13);
    position: absolute;
    transform: translate(-50%,-50%);
    top: 50%;
    left: 50%;
    border-radius: 10px;
    backdrop-filter: blur(10px);
    border: 2px solid rgba(255,255,255,0.1);
    box-shadow: 0 0 40px rgba(8,7,16,0.6);
    padding: 50px 35px;
}
.form *{
    font-family: 'Poppins',sans-serif;
    color: #080101;
    letter-spacing: 0.5px;
    outline: none;
    border: none;
}
.form h3{
    font-size: 32px;
    font-weight: 500;
    line-height: 42px;
    text-align: center;
    color: #000;
}

label{
    display: block;
    margin-top: 30px;
    font-size: 16px;
    font-weight: 500;
    color: #201111;
}
input{
    display: block;
    height: 50px;
    width: 100%;
    background-color: rgba(39, 8, 8, 0.315);
    border-radius: 3px;
    padding: 0 10px;
    margin-top: 8px;
    font-size: 14px;
    font-weight: 300;
}
::placeholder{
    color: #e5e5e5;
}
.button{
    margin-top: 50px;
    width: 100%;
    background-color: #201111;
    color: #ffffff;
    padding: 15px 0;
    font-size: 18px;
    font-weight: 600;
    border-radius: 5px;
    cursor: pointer;
}
.social{
  margin-top: 30px;
  display: flex;
}
.social div{
  background: red;
  width: 150px;
  border-radius: 3px;
  padding: 5px 10px 10px 5px;
  background-color: rgba(255,255,255,0.27);
  color: #eaf0fb;
  text-align: center;
}
.social div:hover{
  background-color: rgba(255,255,255,0.47);
}
.social .fb{
  margin-left: 25px;
}
.social i{
  margin-right: 4px;
}

</style>