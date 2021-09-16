<template>
  <div id="app">
    <div id="nav">
          <h4>Nav</h4>
          <router-link to="/courses" title="Courses">
             <div class="router-container">
            </div>
          </router-link>
          <router-link to="/" title="Main Page">
             <div class="router-container">
            </div>
          </router-link>
    </div>
    <router-view/>
  </div>
</template>

<script>

export default {
}

</script>


<style lang="scss">


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #F6F6F6 ;
}

#nav {
  left: 0;
  top: 0;
  position: fixed;
  background-color: #1261A0;
  width: 70px;
  height: 100%;

  h4 {
    color: white;
    margin-top: 3px;
  }
  
  .router-container {
    height: 50px;
    width: 50px;
    margin: 10px;
    background-color: #288FE0;
    border-radius: 10px;
    cursor: pointer;
  }
}
</style>
