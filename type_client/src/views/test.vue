<template>
  <div class="test">
    <h1>This is test page</h1>
    <h3>User list</h3>
    <div v-for="username in userdata" :key="username">
    <p>{{username.username}}</p>
    </div>
    <button @click="logout">Log out</button>
  </div>
</template>
<script>
import socket from '../config/socket'
export default {
    name: 'test',
    data () {
        return {
            userdata: []
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
