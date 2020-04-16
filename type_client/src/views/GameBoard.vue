<template>
  <div>
    <div class="game-board">
      <div class="row">
        <!-- ini cardnya buat di looping -->
        <Card v-for="user in userdata" :key="user.username" :user="user" />
        <!-- -------- -->
      </div>
      <div class="text-box">
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </p>
      </div>
      <form>
        <div class="form-row align-items-center justify-content-center">
          <div class="col-md-10">
            <input type="text" class="form-control"       id="inlineFormInputName" placeholder="Input your answer here buddy!">
          </div>
          <div class="col-auto my-1">
            <button type="submit" class="btn btn-primary">Submit</button>
          </div>
        </div>
      </form>
      <button @click="rightAnswer">Test</button>
      <button @click.prevent="logout">logout</button>
    </div>
  </div>
</template>

<script>
import Card from '../components/Card'
import socket from '../config/socket' 
export default {
  name: 'GameBoard',
  components: {
    Card
  },
  data () {
      return {
          userdata: []
      }
  },
  methods: {
      logout () {
        //   let uname = localStorage.username
            this.$router.push('/')
            localStorage.removeItem('username')
        },
        rightAnswer () {
            this.userdata.forEach(element => {
                if(localStorage.username == element.username){
                    element.score += 10
                }
            });
                    socket.emit('correct',this.userdata)
                    socket.on('correct',(data)=>{
                        this.userdata = data
                    })
        }
  },
  created () {
      socket.on('user-join',(data)=>{
            this.userdata = data
            console.log(this.userdata)
        })
  }
}
</script>

<style scoped>
.game-board{
  width: 100vw;
  height: 100vh;
  background: #15a7b6;
  padding: 30px 100px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.row{
  width: 100%;
  height: 50%;
  margin: 0;
  display: flex;
  justify-content: center;
}

.text-box{
  width: 100%;
  height: 45%;
  border: 3px ;
  border-style: solid;
  border-color: #52c253;
  border-radius: 20px;
  background: #2ca53e;
  padding: 20px;
  font-size: 25px;
  text-align: left;
  color: #fce669;
}

</style>
