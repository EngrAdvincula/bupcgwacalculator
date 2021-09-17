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
            <input class="grade-input" type="number" placeholder="Input Grades" v-model="newGrade" :style="{borderColor: showError}">
          </div>
          <div class="units-container"> 
            <p>Units</p>
            <input type="number" placeholder="Input Units" v-model="newUnit" @keyup.enter="addValues(); calculateGWA()" :style="{borderColor: showError}">
          </div>
        </div>
      </div>

      <button class="register-btn" @click="addValues(); calculateGWA()" :disabled="isDisabled" :style="{backgroundColor: isDisabledColor}">
        REGISTER
      </button>

      <div class="result">
        <h5>Your GWA is</h5>
        <h4 :style="{color: changeColor}">{{gwa}}</h4>
      </div>

      <div class="grandun-label">
        <h6>Grades</h6> <h6>Units</h6>
      </div>

      <div class="gradesUnitsContainer" v-for="(data, ind) in this.allData" :key="data.id">
          <h5 class="grade">{{data.grade}}</h5>
          <h5 class="unit">{{data.unit}}</h5>
          <button class="update" v-on:click="editValues(ind);calculateGWA()"></button>
          <button class="delete" v-on:click="removeValues(ind); calculateGWA()"></button>
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
        allData: [],
        newID: 1,
        newUnit: null,
        newGrade: null,
        gwa: 'your GWA is...'
      }
    },
  computed: {
    checkIfNaN: function() {
      if (this.gwa = NaN) {
        return this.gwa = 0;
      }
    },
    changeColor: function() {
            if (this.allData.length > 1) {
                return '#1261A0'
            } else {
                return "#70befd"
            }
        },
    isDisabled: function() {
      if (this.newGrade < 1 || this.newGrade > 5 || this.newUnit < 1) {
                return true
            } else {
                return false
            }
    },
    isDisabledColor: function() {
      if (this.newGrade < 1 || this.newGrade > 5 || this.newUnit < 1) {
                return 'rgb(236, 236, 236)'
            } else {
                return '#CEE9FF'
            }
    },

    showError: function() {
      if (this.newGrade < 1 || this.newGrade > 5) {
                return 'red'
            } else {
                return 'green'
            }
    }
  },
  methods: {
    addValues: function() {
            return this.allData.unshift ({id: this.newId++, grade: parseFloat(this.newGrade), unit: parseFloat(this.newUnit), mult: this.newGrade * this.newUnit}),
            this.newUnit = '', this.newGrade = '',

            document.getElementsByClassName('grade-input')[0].focus()
        },
    calculateGWA: function() {

            const GWA = Object.values(this.allData).reduce((a, {mult}) => a + mult, 0)/
                        Object.values(this.allData).reduce((a, {unit}) => a + unit,0)

            return this.gwa = GWA.toFixed(3)
        },
    removeValues: function(ind) {
            this.allData.splice(ind,1)
        },
    editValues: function(ind) {
            return this.newGrade = this.allData[ind].grade, this.newUnit = this.allData[ind].unit,
            this.allData.splice(ind,1)
    },
  }
}
</script>

<style lang="scss">
@import '@/styleSass/mixins.scss';

  .Main-container {
    background-color: #F6F6F6 ;
    width: 100%;
    height: 100vh;
    margin-left: 70px;
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
      margin-top: 2%;
      border-radius: 10px;
      @include center-div;
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
      @include center-div;
      @include main-calc-container;
      
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
             text-indent: 10px;
             outline: none;
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
             text-indent: 10px;
             outline: none;
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
      @include main-calc-container;
      @include center-div;
      position: relative;
      width: 600px;
      height: 80px;
      margin-top: 20px;
      display: flex;

      h4 {
        position: absolute;
        font-weight: bold;
        color: $primary-color;
        top: 30%;
        right: 18%;
      }

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
      margin-top: 20px;
      display: flex;
      @include main-calc-container;
      @include center-div;
      h6 {
        padding: 5px 100px;
        color: #1261A0;
      }
    }
    
    .gradesUnitsContainer {
      @include main-calc-container;
      @include center-div;
      margin-top: 10px;
      height: 70px;
      display: flex;
      position: relative;

      .grade {
        font-weight: bold;
        position: absolute;
        top: 30%;
        left: 20%;
        color: #1261A0;
      }

      .unit {
        color: #1261A0;
        font-weight: bold;
        position: absolute;
        top: 30%;
        right: 37%;
      }

      .update {
        position: absolute;
        width: 35px;
        height: 35px;
        background-color: #A2D5F2;
        border-radius: 50%;
        border: none;
        background-image: url(edit.png);
        background-repeat: no-repeat;
        background-size: 20px 20px;
        background-position: center;
        right: 15%;
        top: 22%;

        &:hover {
          background-color: #07689F;
          cursor: pointer;
        }
      }

      .delete {
        position: absolute;
        width: 35px;
        height: 35px;
        background-color: #F37777;
        border-radius: 50%;
        border: none;
        background-image: url(whitecross.png);
        background-repeat: no-repeat;
        background-size: 20px 20px;
        background-position: center;
        right: 7%;
        top: 22%;
        &:hover {
          background-color: #FE0909;
          cursor: pointer;
        }
      }

    }

  }

  @media screen and (max-width:741px) {
    .Main-container {
      .title {
        width: auto;
      }

      .input-calc {
        width: auto;
        .input-calc-container {
          margin-left: auto;
          margin-right: auto;
        }
      }

      .register-btn {
        width: auto;
      }

      .result {
        width: auto;
        h4 {
          right: 10%;
        }
      }

      .grandun-label {
        width: auto;
        h6 {
          width: 15%;
        }
      }

      .gradesUnitsContainer {
        width: auto;
      }
    }
  }

  @media screen and (max-width:583px) {
    .Main-container {

      .top-nav {
        h3 {
          font-size: 16px;
        }
      }

      .input-calc {
        .input-calc-container {
          .grades-container {
            input {
              width: 120px;
            }
          }
          .units-container {
            input {
              width: 120px;
            }
          }
        }
      }

      .register-btn {
        width: auto;
      }

      .result {
        width: auto;
      }

      .grandun-label {
        width: auto;
      }

      .gradesUnitsContainer {
        width: auto;
      }
    }
  }
</style>