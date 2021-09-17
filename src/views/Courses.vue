<template>
  <div class="courses-container">
      <h1>{{ $route.params.name }}</h1>
      <p>Available Year and Sem</p>
       <div v-if="findCourse" class="course-container">
            <div class="one" v-for="one in findCourse.Obj" :key="one.id" >
                <router-link :to="{ name: 'Compute', params: { id: one.id}}" class="go-to-btn"><div class="container-link">
                    <div class="course-name">
                        <h6>{{findCourse.nname}}</h6>
                    </div>
                            <h5>{{ (one.year).toLowerCase() }} Year {{ (one.sem).toLowerCase() }} Sem </h5>
                            <div class="two" v-for="two in one.subjects" :key="two.id">
                                {{ two.sub }}
                            </div>
                        </div></router-link>
                    </div>
        </div>
  </div>
 
</template>

<script>
export default {
    name: 'Courses',
    computed: {
        findCourse() {
            return this.$store.getters.findCourse(this.$route.params.name)
        }
    }
}
</script>

<style lang="scss">
@import '@/styleSass/mixins.scss';

    .courses-container {
        background-color: #faf9f9 ;
        width: 100%;
        height: 100%;
        margin-left: 70px;
        padding-bottom: 10%;
        
        h1 {
            text-align: left;
            color: $primary-color;
            margin-left: 11%;
            padding-top: 5%;
            font-weight: bold;
        }

        p {
            text-align: left;
            color: #626262;
            margin-left: 11%;
            line-height: 10%;
        }

        .course-container {
            display: flex;
            flex-wrap: wrap;
            margin-left: 5%;
            margin-right: 10%;
            .one {
                
                .go-to-btn {
                    text-decoration: none;
                .container-link {
                    position: relative;
                    margin-bottom: 20px;
                    margin-top: 20px;
                    background-color: white;
                    width: 320px;
                    height: 350px;
                    border-radius: 10px;
                    margin-left: 10px;
                    padding-top: 20px;
                    
                    &:hover {
                        background-color: rgb(238, 238, 238);
                    }
                
                .course-name {
                    border-radius: 25px;
                    background-color: $primary-color;
                    height: 25px;
                    width: 260px;
                    margin-left: 30px;
                    margin-bottom: 20px;
                    padding-top: 3px;

                        h6 {
                            color: white;
                            font-weight: bold;
                            padding: 0 20px;
                        }
            }

                .go-to-btn {
                    position: absolute ;
                    left: 20px;
                }

                h5 {
                    text-align: left;
                    margin-left: 30px;
                    font-weight: bold;
                    color: #626262;
                }

                .two {
                    text-align: left;
                    padding-left: 30px;
                    color: #626262;
                }
                }
                }

            }
        }

    }
    

    strong {
        font-size: 20px;
    }
</style>