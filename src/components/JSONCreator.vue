<template>
  <div class="container">
      <p>Course</p><input type="text" name="course" v-model="course"><button>Register Course</button>
      <p>Year</p><input type="number" name="semester" v-model="year">
      <p>Sem</p><input type="number" name="year" v-model="sem">
      <h1>Subject and Units</h1>
      <p>Subject</p> <input type="text" name="subjectName" v-model="newSubject">
      <p>Equivalent Units</p> <input type="number" name="equivalentUnits" v-model="newUnits">
      <button @click="addSubject()">Add</button>

        

      <ul v-for="data in allSubjects" :key="data.sub">
          <li>{{data.sub}}, {{data.units}}</li>
      </ul>
      <button @click="addYearAndSem()">Register</button>
      <div class="yearAndSemData" v-for="info in wholeData" :key="info.id">
          <h3>{{info.year}}ST YEAR {{info.sem}}ST SEM</h3>
          <ul v-for="subs in info.subjects" :key="subs.sub">
              <li>{{subs.sub}}</li>
          </ul>
      </div>
      <button @click="courseJSONFromatter()">RENDER</button>
      <h3>{{courseData}}</h3>
      <!-- <button @click.prevent="sendPost()">Upload</button> -->
  </div>
</template>

<script>
// import axios from 'axios'

export default {
    name: 'JSONCreator',
    data() {
        return {
            courseData: [],
            wholeData: [],
            allData: [],
            allSubjects: [],
            course: null,
            year: null,
            sem: null,
            yearAndSemId: 1,
            courseId: 1,
            newSubject: null,
            newUnits: null,
        }
    },
    methods: {
        addSubject: function(){
            return this.allSubjects.push({sub: this.newSubject, units: parseFloat(this.newUnits), grades: null}),
            this.newSubject = '', this.newUnits = ''
        },
        addYearAndSem: function() {
            return this.allData.push({id: this.yearAndSemId++, year: parseInt(this.year), sem: parseInt(this.sem), subjects: this.allSubjects}),
            this.wholeData.push(...this.allData),
            this.year = '', this.sem = '', this.allData = [], this.allSubjects = []
        },
        courseJSONFromatter: function() {
            return this.courseData.push({id: this.courseId++, name: this.course, Obj: this.wholeData})
        }
        // sendPost() {
        //     const postData = this.allData;
        //     axios
        //         .post('http://127.0.0.1:8000/gwacalculator/subject-create/', postData)
        //         .then(res => {
        //             console.log(res.body)
        //         })
            
        // }
    }
}
</script>

<style>

</style>