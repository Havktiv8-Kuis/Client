<template>
  <div class="game">
    <h1>This is game page</h1>
    <h3>User list</h3>
    <div v-for="username in userdata" :key="username">
    <p>{{username}}</p>
    </div>
    <button @click="logout">Log out</button>
  </div>
</template>
<script>
import socket from '../config/socket'
export default {
    name: 'game',
    data () {
        return {
            userdata: []
        }
    },
    created () {
        if(!localStorage.username) {
            this.$router.push('/')
        }
    },
    methods: {
        logout () {
            localStorage.removeItem('username')
            this.$router.push('/')
            socket.emit('disconnect')
        }
    },
    created () {
        socket.on('user-join',(data)=>{
            this.userdata = data
        })
    }
}
</script>
