<template>
  <div class="hello">
        <h1>Courses</h1>
        <p>Choose your Course to display Year, Sem and Subjects</p>
        <table>
            <tr>
              <th>Course</th>
              <th class="mobile">Department</th>
              <th class="mobile">Available Year and Sem</th>
            </tr>
            <tr v-for="course in courses" :key="course.id">
              <td><strong><router-link :to="{ name: 'Courses', params: { name: course.name } }">{{course.name}}</router-link></strong></td>
              <td class="mobile">{{course.dept}}</td>
              <td class="mobile">{{course.yearAndSemCount}}</td>
            </tr>
        </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  // props: {
  //   msg: String
  // },
  data() {
    return {
      yearAndSemCount: []
    }
  },
  computed: {
    courses() {
      return this.$store.getters.courses
    }
  },
  methods: {
    async getData() {
      try {
        const response = await axios.get(
          "http://127.0.0.1:8000/gwacalculator/subject-list?course=BSCpE" 
        );
        // JSON responses are automatically parsed.
        this.posts = response.data;
      } catch (error) {
        console.log(error);
      }
    },
  }
}
</script>


<style lang="scss">

  .hello {
    background-color: white ;
    height: 100vh;
    width: 100vw;
    margin-left: 70px;
    h1 {
      margin-top: 4%;
    }
    h1, p {
      font-weight: bold;
      color: #1261A0;
      text-align: left;
      margin-left: 10%;
    }
    p {
      color: #626262;
      font-weight: 300;
      margin-bottom: 2%;
    }

    table {
      border-collapse: collapse;
      width: 80%;
      margin-left: 10%;
    th, td {
      padding: 14px;
      text-align: left;
      border-bottom: 1px solid #ddd;
      }
    }
  }

  @media screen and (max-width: 540px) {
    .mobile {
      display: none;
    }
  }

</style>