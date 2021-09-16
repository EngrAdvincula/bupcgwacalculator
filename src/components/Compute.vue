<template>
  <div class="container">
      <div class="compute-title">
          <div class="course">
              {{this.$route.params.name}}
          </div>
          <div class="your-gwa">
              <h4>your GWA is <span>{{total}}</span></h4>
          </div>
      </div>

      <div v-for="subs in findSemYear.subjects" :key="subs.sub" class="subs-container">
          <h5>{{ subs.sub }} </h5> <input type="number" name="" id="" v-model="subs.grades" placeholder="Input Grades">
          <p>Equivalent Unit: {{subs.units}}</p>
      </div>
      <button @click="computedGWA" class="compute-btn" >Compute</button>
  </div>
</template>

<script>
export default {
    name: 'Compute',
    computed: {
        findSemYear() {
            return this.$store.getters.findSemYear((parseInt(this.$route.params.id)), this.$route.params.name )
        }
    },
    data() {
        return{
            data: this.$store.state.courses.find(course => course.name == this.$route.params.name).Obj.find(course => course.id == this.$route.params.id).subjects,
            total: ''
        }
    },
    methods: {
            computedGWA: function() {

            /* Trying to use ES6 Reduce for a more elegant code**/

               let gradesTimesUnits = 0
               

                for (let i in this.data) {
                    //This if loop is to make all no entries 0 so that the users can see their tentative GWA
                    if (this.data[i].grades === '') {
                        this.data[i].grades = "0"
                        this.data[i].units = "0"
                    }
                    gradesTimesUnits += (parseFloat(this.data[i].grades) * parseFloat(this.data[i].units))
                }

                const totalUnits = Object.values(this.data).reduce((a, {units}) => a + parseFloat(units) ,0)

                return this.total = (gradesTimesUnits/totalUnits).toFixed(3)

            }
        }
}
</script>

<style lang="scss">
@import '@/styleSass/mixins.scss';

.container {
    background-color: #F6F6F6 ;
    height: 100vh;
    width: 100vw;
    .compute-title {
        @include center-div;
        @include main-calc-container;
        height: 100px;
        position: relative;
        margin-top: 3%;

        .course {
            position: absolute;
            background-color: $primary-color;
            color: white;
            width: 200px;
            border-radius: 20px;
            font-weight: bold;
            line-height: 120%;
            padding: 5px;
            top: 23%;
            left: 7%;
        }

        .your-gwa {
            position: absolute;
            color: $primary-color;
            top: 35%;
            right: 7%;
            h4 {
                span {
                    font-weight: bold;
                }
            }
        }
    }

    .subs-container {
        @include center-div;
        @include main-calc-container;
        height: 70px;
        margin-top: 10px;
        position: relative;

        h5 {
            position: absolute;
            font-weight: bold;
            color: $primary-color;
            top: 20%;
            left: 8%;
        }

        p {
            position: absolute;
            left: 8%;
            top: 52%;
            color: #b6b6b6;
        }

        input {
            position: absolute;
            top: 20%;
            right: 5%;
            @include inputDesign;
            border-radius: 5px;
            height: 38px;
            width: 150px;
            
        }
    }

    .compute-btn {
        background-color: #CEE9FF;
        border: 2px solid #1261A0;
        width: 600px;
        height: 50px;
        border-radius: 10px;
        margin-top: 20px;
        color: #1261A0;
        font-weight: bold;
    }
}


</style>