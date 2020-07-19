<template>
  <ul class="d-flex flex-wrap">
    <div>
      <button v-on:click="getCourseData">Get Course Data</button>
    </div>
    <li v-for="courseData in courseDataList" :key="courseData.id" class="col-md-3 mx-auto scratch-no-1">
      <div class="card">
        <div class="card-header d-flex align-items-center"><img class="img-fluid course-logo" src="../assets/images/logos/scratch-logo.png"><span class="ml-3 course-title">{{courseData.name}}</span></div>
        <div class="card-body">
          <div>
            <b-button id="show-btn" @click="$bvModal.show('courseDescription')"><img class="img-fluid" v-bind:src="courseData.image"></b-button>
            <b-modal size="lg" id="courseDescription" hide-footer>
              <template v-slot:modal-title>
                <div class="d-flex align-items-center"><img class="img-fluid course-logo" src="../assets/images/logos/scratch-logo.png"><span class="ml-3 course-title">{{courseData.name}}</span></div>
              </template>
              <div class="d-flex">
                <div class="course-image">
                  <a href="https://scratch.mit.edu/projects/editor/?tutorial=getStarted" target="_blank"><img class="img-fluid" src="../assets/images/scratch/como_comenzar.jpg"></a>
                </div>
                <div class="course-description d-flex flex-column justify-content-between w-100 px-3">
                  <div>
                    <p class="decription-text">{{courseData.description}}</p>
                  </div>
                  <div>
                    <div class="couse-level"><small>{{courseData.level}}</small></div>
                    <a v-bind:href="courseData.url" target="_blank">Ir al curso</a>
                  </div>
                </div>
              </div> 
                <b-button class="mt-3 w-auto float-right" block @click="$bvModal.hide('courseDescription')">Volver</b-button>
            </b-modal>
          </div>
        </div>
        <div class="card-footer"><span class="course-type float-left"></span><span class="course-level float-right">{{courseData.level}}</span></div>
      </div>
    </li>
  </ul>
</template>

<script>
  import axios from 'axios';
  export default {
    name: "Course",
    data() {
      return {
        courseDataList: []
      };
    },
    methods: {
      getCourseData() {
        // fetch("course.json")
        // .then(response => response.json())
        // .then(data => (this.courseDataList = data));
        axios.get("course.json").then(response => (this.courseDataList = response.data));
      }
    }
  }
</script>
<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Cabin+Sketch&family=Poppins:wght@400;700&display=swap');

  $blue: #282C82;
  $purple: #4F539E;
  $purple-light: #A5B4E5;
  $yellow: #F8EB7C;
  $light: #FAF6F6;

  #learning-options {
    background-color: $blue;
    padding: 2rem 0;
    li {
      list-style: none;
    }
    .card {
      .card-header {
        .course-logo {
          max-width: 40px;
          float: left;
        }
      }
      .card-body {
        padding: 0;
        button {
          padding: 0;
          border: none;
        }
      }
      .card-footer {
        .course-type {
          background-color: transparent;
          width: 0;
          height: 0;
          border-left: 20px solid transparent;
          border-right: 20px solid transparent;
          border-bottom: 30px solid #F8EB7C
        }
      }
    }
  }
  #courseDescription {
    font-size: 1.2em;
    .course-logo {
      max-width: 40px;
      float: left;
    }
    .modal-body {
      .course-image {
        img {
          max-width: 250px;
        }
      }
    }
  }
</style>