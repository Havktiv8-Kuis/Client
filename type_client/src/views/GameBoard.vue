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
          {{sentence}}
        </p>
      </div>
      <form>
        <div class="form-row align-items-center justify-content-center">
          <div class="col-md-10">
            <input type="text" class="form-control" id="inlineFormInputName" placeholder="Input your answer here buddy!" v-model="answer">
          </div>
          <div class="col-auto my-1">
            <button type="submit" class="btn btn-primary" @click.prevent="checkAnswer" >Submit</button>
          </div>
        </div>
      </form>
      <!-- <button @click="rightAnswer">Test</button> -->
      <button @click.prevent="logout">logout</button>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2'
import socket from '../config/socket'
import Card from '../components/Card'
// import socket from '../config/socket' 
export default {
  name: 'GameBoard',
  components: {
    Card
  },
  data () {
    return {
      word: '',
      answer: '',
      userdata: [],
      sentence: '',
    }
  },
  methods: {
    getWord () {
      this.answer = ''
      socket.emit('get-word')
      socket.on('get-word', (data) => {
        this.word = data
        this.sentence = data.sentence
      })
    },
    // checkWord () {
    //   if (this.word.toLowerCase() === this.answer.toLowerCase() && this.word != '') {
    //     this.getWord()
    //   } else {
    //     console.log('Wrong answer')
    //   }
    // },
    logout () {
      // const name = localStorage.username
      // socket.emit('exit',name)
      localStorage.removeItem('username')
      this.$router.push('/')
        // localStorage.clear()
    },
    checkAnswer () {
      if (this.word.answer.toLowerCase() === this.answer.toLowerCase()) {
        this.userdata.forEach(element => {
          if(localStorage.username == element.username) {
            element.score += 10
          }
        });
        socket.emit('correct',this.userdata)
        socket.on('user-join',(data)=>{
            this.userdata = data
        })
        let user = this.userdata.find(el => el.username == localStorage.username)
        if (user.score >= 50) {
          this.winner()
        } else {
          this.getWord()
        }
      } else {
        console.log('Wrong answer')
        this.answer = ''
      }
    },
    rightAnswer () {
      this.userdata.forEach(element => {
        if(localStorage.username == element.username){
            element.score += 10
        }
      });
      socket.emit('correct',this.userdata)
      socket.on('user-join',(data)=>{
          this.userdata = data
      })
    },
    winner () {
      socket.emit('winner', localStorage.username)
      socket.on('winner', (name) => {
        Swal.fire({
          position: 'top',
          icon: 'success',
          title: `The winner is ${name}`,
          showConfirmButton: false,
          timer: 5000
        })
      })
    }
  },
  created() {
    if (!localStorage.username) {
      this.$router.push('/')
    } else {
      socket.on('user-join',(data)=>{
        this.userdata = data
        // console.log(this.userdata)
        if (this.userdata.length > 1) {
          this.getWord()
        }
      })
    }
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