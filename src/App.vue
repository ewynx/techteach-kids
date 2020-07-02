<template>
  <div id="app">
    <header role="banner">
      <div>
        <b-navbar toggleable="lg">
          <b-navbar-brand href="#" class="logo d-flex align-items-center" aria-label="Tech Teach Logo">
            <img class="img-fluid" src="./assets/images/tech-teach-logo.png" style="width: 60px;">
            <div class="d-flex flex-column logo-text ml-3">
              <div>TechTeach</div>
              <div><small>Latinoamérica</small></div>
            </div>
          </b-navbar-brand>
          <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
          <b-collapse id="nav-collapse" class="justify-content-end" is-nav>
            <b-navbar-nav>
              <b-nav-item href="#learn">Aprende</b-nav-item>
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
        <article class="question">
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
        <article class="menu-learning-option">
          <div class="row flex-column flex-md-row justify-content-around">
            <div class="col-md-3 mx-auto text-center"><button class="programming-link">Programar</button></div>
            <div class="col-md-3 mx-auto text-center"><button class="typing-link">Type</button></div>
            <div class="col-md-3 mx-auto text-center"><button class="google-drive-link">Google Drive</button></div>
          </div>
        </article>
        <article class="learning-options">
          <div class="ul d-flex flex-wrap">
            <div class="li col-md-3 mx-auto scratch-no-1">
              <div class="card">
                <div class="card-header">Fácil <img class="img-fluid course-logo" src="./assets/images/scratch/scratch.jpg"></div>
                <div class="card-body">
                  <div>
                    <b-button id="show-btn" @click="$bvModal.show('bv-modal-example')"><img class="img-fluid" src="./assets/images/scratch/como_comenzar.jpg"></b-button>
                    <b-modal id="bv-modal-example" hide-footer>
                      <template v-slot:modal-title>
                        ¿Cómo comenzar?
                      </template>
                      <div class="d-block text-center">
                        <div>
                          <a href="https://scratch.mit.edu/projects/editor/?tutorial=getStarted" target="_blank"><img class="img-fluid" src="./assets/images/scratch/como_comenzar.jpg"></a>
                        </div>
                        <div>
                          Lorem ipsum
                        </div>
                      </div>
                        <b-button class="mt-3" block @click="$bvModal.hide('bv-modal-example')">Close Me</b-button>
                    </b-modal>
                  </div>
                </div>
                <div class="card-footer text-center">¿Cómo comenzar?</div>
              </div>
            </div>
          </div>
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
  export default {
    name: 'app',
    components: {
      ChatBox
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
  .question {
    background-color: $yellow;
    h1 {
      color: $blue;
      font-family: 'Cabin Sketch', cursive;
      font-weight:  400;
      font-size: 2.6667em;
    }
  }
  .menu-learning-option {
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
  .learning-options {
    background-color: $blue;
    padding: 2rem 0;
    .card {
      .card-header {
        .course-logo {
          max-width: 40px;
          float: right;
        }
      }
      .card-body {
        padding: 0;
        button {
          padding: 0;
          border: none;
        }
      }
    }
  }
</style>

