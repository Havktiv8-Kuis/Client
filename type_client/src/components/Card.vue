<template>
  <div class="card">
        <img src="../assets/user.svg" alt="user-image">
        <h3>{{user.username}}</h3>
        <h5>Score:</h5>
        <p>{{user.score}}</p>
  </div>
</template>

<script>
import socket from '../config/socket'
export default { 
  name: 'Card',
  props:['user'],
  data () {
    return {
        userdata: []
    }
  },
  created () {
        socket.on('user-join',(data)=>{
            this.userdata = data
        })
    }
}
</script>
    
<style scoped>
.card{
  width: 12rem;
  height: 100%;
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  border: 3px ;
  border-style: solid;
  border-color: #ffc150;
  border-radius: 20px;
  margin-right: 30px;
  background: #fce669;
}

.card img{
  width: 100px;
  margin-bottom: 15px;
}

.card h3{
  color: #cb4a39;
}

.card h5{
  margin: 0;
  color: #9e6c36;
}

.card p{
  font-size: 4rem;
  margin: 0;
  color: #774b30;
}
</style>
