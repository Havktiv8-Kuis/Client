<template>
  <div class="home">
    <div class="container">
      <div class="img">
        <img src="../assets/game.svg">
      </div>
      <div class="signin-container">
        <form id="signin-form" @submit.prevent="login">
          <img class="avatar" src="../assets/avatar.svg">
          <h2>Let's Play!</h2>
          <div class="input-div one">
            <div class="i">
              <i class="fas fa-at"></i>
            </div>
            <div>
              <input
              v-model="username"
              id="username"
              type="text"
              class="input"
              placeholder="Username"
              required
              >
            </div>
          </div>
          <input type="submit" class="btn" value="Join">
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import socket from '../config/socket'
export default {
  name: 'Home',
  data () {
    return {
      username: ''
    }
  },
  components: {

  },
  methods: {
    login () {
      const userdata = {
        username: this.username,
        score: 0
      }
      socket.emit('user-join', userData)
      socket.on('user-list', (condition) => {
        if (condition) {
          localStorage.setItem('username', this.username)
          this.$router.push('/game')
        } else {
          console.log('user already exist')
        }
      })
    }
  },
  created() {
    if(localStorage.username) {
      this.$router.push('/game')
    }
  }
}
</script>

<style scoped>
.home .container {
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 15rem;
  padding: 0 2rem;
  font-weight: 600;
}

.signin-container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  text-align: center;
}

#signin-form {
  width: 360px;
}

#signin-form h2 {
  font-size: 2.9rem;
  text-transform: uppercase;
  margin: 15px 0;
  font-weight: 600;
  color: #333;
}

.img {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.img img {
  width: 500px;
}

.avatar {
  width: 100px;
}

.input-div {
  display: grid;
  grid-template-columns: 7% 93%;
  margin: 25px 0;
  padding: 5px 0;
  border-bottom: 2px solid #d9d9d9;
}

.input-div .i i {
  color: rgb(83, 24, 179);
}

.input-div.one {
  margin-top: 0;
}

.input-div.two {
  margin-bottom: 4px;
}

.i {
  display: flex;
  justify-content: center;
  align-items: center;
}

.i i {
  color: #d9d9d9;
}

.input-div>div {
  position: relative;
  height: 45px;
}

.input,
.form-control {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  border: none;
  outline: none;
  background: none;
  padding: 0.5rem 0.7rem;
  font-size: 1.2rem;
  color: #555;
}

.option {
  display: block;
  text-align: right;
  text-decoration: none;
  color: #999;
  font-size: 0.9rem;
  transition: .3s;
}

.option a {
  color: #333;
}

.option a:hover {
  color: rgb(83, 24, 179);
  text-decoration: none;
  cursor: pointer;
}

.btn {
  display: block;
  width: 100%;
  height: 50%;
  border-radius: 25px;
  margin: 1rem 0;
  font-size: 1.2rem;
  outline: none;
  border: none;
  background-image: linear-gradient(to right, #a8a8a8, #919191, #a8a8a8);
  cursor: pointer;
  color: #fff;
  background-size: 200%;
  transition: .5s;
}

.btn:hover {
  background-position: right;
  color: #fff;
}

@media screen and (max-width: 1050px) {
  .home .container {
    grid-gap: 5rem;
  }
}

@media screen and (max-width: 1000px) {
  #signin-form{
    width: 290px;
  }

  .home .container{
    justify-content: center;
  }

  .signin-container h2 {
    font-size: 2.4rem;
    margin: 8px 0;
  }
  .img img {
    width: 400px;
  }
}

@media screen and (max-width: 900px) {
  .home .container {
    grid-template-columns: 1fr;
    justify-content: center;
  }
  .img {
    display: none;
  }
  .signin-container {
    justify-content: center;
  }
}
</style>
