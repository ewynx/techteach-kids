<template>
  <div id="app">
    <header role="banner">
      <div>
        <b-navbar toggleable="lg">
          <b-navbar-brand href="#" class="logo d-flex align-items-center" aria-label="Tech Teach Logo">
            <img class="img-fluid" src="./assets/images/tech-teach-logo.png" style="width: 60px;">
            <div class="d-flex flex-column logo-text ml-3">
              <div>TechTeach</div>
              <div><small>Aprende a programar y diviertete</small></div>
            </div>
          </b-navbar-brand>
          <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
          <b-collapse id="nav-collapse" class="justify-content-end" is-nav>
            <b-navbar-nav>
              <b-nav-item href="#learn">Aprende</b-nav-item>
              <b-nav-item-dropdown text="Los cursos">
                <b-dropdown-item href="#">Programar</b-dropdown-item>
                <b-dropdown-item href="#">Type</b-dropdown-item>
                <b-dropdown-item href="#">Google Drive</b-dropdown-item>
              </b-nav-item-dropdown>
              <b-nav-item href="#learn">Tutores</b-nav-item>
              <b-nav-item href="#learn">Conócenos</b-nav-item>
            </b-navbar-nav>
          </b-collapse> 
        </b-navbar>
      </div>
    </header>
    <section role="section">
      <div class="sub-header">
        <div class="text-center">
          <img alt="sub-header" class="img-fluid mx-auto" src="./assets/images/sub-header.jpg">
        </div>
      </div>
    </section>
    <main role="main">
      <section role="section">
        <article id="question">
          <div class="container">
            <div class="row align-items-center">
              <div class="col-8 col-md-4 col-lg-3 px-5 mx-auto">
                <a class="chatbot-link" href="#">
                  <img alt="chatbot" src="./assets/images/chatbot/SambotNormal-01.svg">
                </a>
              </div>
              <div class="col-12 col-md-8 col-lg-9">
                <h1 class="learn-question text-center">¿Qué aprenderemos hoy?</h1>
              </div>
            </div>
          </div>
        </article>
        <article id="menu-learning-option">
          <div class="row flex-column flex-md-row justify-content-around">
            <div class="col-md-3 mx-auto text-center"><button class="programming-link">Programar</button></div>
            <div class="col-md-3 mx-auto text-center"><button class="typing-link">Type</button></div>
            <div class="col-md-3 mx-auto text-center"><button class="google-drive-link">Google Drive</button></div>
          </div>
        </article>
        <article id="learning-options">
          <Courses />
        </article>
      </section>
    </main>
    <footer>
      
    </footer>

  <!--This is what it's really about!-->
    <ChatBox class="fixed-bottom mb-5"/>
  </div>
</template>

<script>
  import ChatBox from './components/ChatBox.vue'
  import Courses from './components/courses.vue'
  export default {
    name: 'app',
    components: {
      ChatBox,
      Courses
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

  #app {
    font-family: 'Poppins', sans-serif;
    font-weight: 400;
    font-size: 18px;
  }
  small {
    font-size: 0.8em;
  }
  strong, b {
    font-weight: 700;
  }
  header {
    nav {
      background-color: $purple-light;
      .logo-text {
        color: $blue;
        font-weight: 700;
      }
      .nav-link {
        color: $blue !important;
        font-weight: 700;
        &:hover, &:active {
          border-bottom: 2px solid $yellow;
        }
      }
    }
  }
  .sub-header {
    background-color: $blue;
  }
  #question {
    background-color: $yellow;
    h1 {
      color: $blue;
      font-family: 'Cabin Sketch', cursive;
      font-weight:  400;
      font-size: 2.6667em;
    }
  }
  #menu-learning-option {
    background-color: $light;
    padding: 2rem 0;
    button {
      font-weight: 700;
      border: none;
      &.programming-link {
        background-color: transparent;
        color: $purple;
        width: 0;
        height: 0;
        border-left: 100px solid transparent;
        border-right: 100px solid transparent;
        border-bottom: 150px solid $yellow;
        line-height: 150px;
      }
      &.typing-link {
        background-color: $purple-light;
        color: $blue;
        height: 150px;
        width: 150px;
        border-radius: 50%;
      }
      &.google-drive-link {
        background-color: $purple;
        color: $yellow;
        height: 150px;
        width: 150px;
      }
    }
  } 
</style>

