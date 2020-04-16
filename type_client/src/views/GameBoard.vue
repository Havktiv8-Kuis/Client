<template>
  <div>
    <div class="game-board">
      <div class="row">
        <!-- ini cardnya buat di looping -->
        <div class="card">
          <img src="../assets/user.svg" alt="user-image">
          <h3>Player 1</h3>
          <h5>Score:</h5>
          <p>70</p>
        </div>
        <!-- -------- -->
        <div class="card">
          <img src="../assets/user.svg" alt="user-image">
          <h3>Player 2</h3>
          <h5>Score:</h5>
          <p>50</p>
        </div>
        <div class="card">
          <img src="../assets/user.svg" alt="user-image">
          <h3>Player 3</h3>
          <h5>Score:</h5>
          <p>10</p>
        </div>
        <div class="card">
          <img src="../assets/user.svg" alt="user-image">
          <h3>Player 4</h3>
          <h5>Score:</h5>
          <p>30</p>
        </div>
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
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameBoard'
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
  height: 45%;
  margin: 0;
  display: flex;
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
