<template>
  <div class="hello">
        <h1>COURSES</h1>
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
    background-color: #F6F6F6 ;
    height: 100vh;
    width: 100vw;
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