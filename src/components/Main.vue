<template>
  <div class="Main-container">
      <div class="top-nav">
        <h3>BUPC Student? Proceed to <router-link to="/courses"> <button class="course-btn">Course</button></router-link></h3>
      </div>

      <div class="title">
        <h3>GWA Calculator</h3>
        <h6>Made with love by: ICpEP.se Dev Team</h6>
      </div>

      <div class="input-calc">
        <div class="input-calc-container">
          <div class="grades-container">
            <p>Grades</p>
            <input type="number" placeholder="Input Grades">
          </div>
          <div class="units-container"> 
            <p>Units</p>
            <input type="number" placeholder="Input Grades">
          </div>
        </div>
      </div>

      <button class="register-btn">
        REGISTER
      </button>

      <div class="result">
        <h5>Your GWA is</h5>
      </div>

      <div class="grandun-label">
        <h6>Grades</h6> <h6>Units</h6>
      </div>
      <!-- <ul v-for="data in this.$store.state.courses.Obj[0]" :key="data.id">
          <li>{{data.subjects}}</li>
      </ul> -->
  </div>
</template>

<script>
export default {
    name: 'Main',
    data() {
      return {
        name: '',
        edad: null
      }
    }
}
</script>

<style lang="scss">
  .Main-container {
    background-color: #F6F6F6 ;
    width: 100%;
    height: 100vh;
      .top-nav {
        background-color: #ffffff ;
        height: 70px;
        .course-btn {
          background-color: #1261A0;
          color: white;
          font-size: 20px;
          padding: 5px 20px;
          border: none;
          border-radius: 20px;
          cursor: pointer;
        }
        h3 {
          font-weight: bold;
          color: #626262;
          padding: 18px;
          font-size: 24px;
        }

      }
    .title {
      height: 100px;
      width: 600px;
      margin-top: 50px;
      border-radius: 10px;
      margin-left: auto;
      margin-right: auto;
      background-color: white ;
        h3 {
          font-weight: bold;
          color: #1261A0;
          padding-top: 20px ;
        }
        h6 {
          color: #1D8FEA;
        }
    }

    .input-calc {
      height: 130px;
      width: 600px;
      margin-top: 20px;
      border-radius: 10px;
      margin-left: auto;
      margin-right: auto;
      background-color: white ;

      .input-calc-container {
        padding-top: 18px;
        display: flex;
        padding-left: 50px;
         .grades-container {
           text-align: left;
           input {
             background-color: #E2F0FB;
             border: none;
             height: 45px;
             width: 230px;
             border-radius: 10px;
           }
         }
         .units-container {
           text-align: left;
           margin-left: 20px;
           input {
             background-color: #E2F0FB;
             border: none;
             height: 45px;
             width: 230px;
             border-radius: 10px;
             color: #A6A6A6;
           }
         }
      }

    }

    .register-btn {
      background-color: #CEE9FF;
      border: 2px solid #1261A0;
      width: 600px;
      height: 50px;
      border-radius: 10px;
      margin-top: 20px;
      color: #1261A0;
      font-weight: bold;
    }

    .result {
      background-color: white;
      margin-left: auto;
      margin-right: auto;
      width: 600px;
      height: 80px;
      border-radius: 10px;
      margin-top: 20px;

      h5 {
        text-align: left;
        padding-left: 100px;
        padding-top: 30px;
        font-weight: bold;
        color: #1261A0;
        font-size: 16px;
      }
    }

    .grandun-label {
      height: 35px;
      width: 600px;
      background-color: white;
      margin-top: 20px;
      border-radius: 10px;
      margin-left: auto;
      margin-right: auto;
      display: flex;
      h6 {
        padding: 5px 130px;
        color: #1261A0;
      }
    }
    
  }
</style>