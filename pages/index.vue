<template>
  <section class="container">
    <div class="spinner" v-if="isLoading">
      <div class="dot1"></div>
      <div class="dot2"></div>
    </div>
    <h1 class="title" v-else>{{ screenResolution }}</h1>
    <footer>
      <p>
        <span>A small experimental project by <a class="underline" href="http://hmatalonga.com/">Hugo Matalonga</a></span>
        <a href="https://twitter.com/hmatalonga" class="twitter-follow-button" data-show-count="false">Follow @hmatalonga</a><script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
      </p>
    </footer>
  </section>
</template>

<script>
export default {
  data () {
    return {
      isLoading: true,
      screen: {
        width: 0,
        height: 0,
      }
    }
  },
  computed: {
    screenResolution () {
      return `${this.screen.width}x${this.screen.height}`
    }
  },
  methods: {
    setViewport () {
        this.screen.width = window.screen.width
        this.screen.height = window.screen.height
        this.isLoading = false
    }
  },
  mounted () {
    this.setViewport()
  }
}
</script>

<style lang="scss" scoped>
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  background: linear-gradient(rgba(0, 0, 0, 0.45),rgba(0, 0, 0, 0.45)),
              url(https://source.unsplash.com/category/nature) no-repeat scroll 50%/cover transparent;
  .spinner {
    margin: 100px auto;
    width: 40px;
    height: 40px;
    position: relative;
    text-align: center;
    
    -webkit-animation: sk-rotate 2.0s infinite linear;
    animation: sk-rotate 2.0s infinite linear;
  }

  .dot1, .dot2 {
    width: 60%;
    height: 60%;
    display: inline-block;
    position: absolute;
    top: 0;
    background-color: white;
    border-radius: 100%;
    
    -webkit-animation: sk-bounce 2.0s infinite ease-in-out;
    animation: sk-bounce 2.0s infinite ease-in-out;
  }

  .dot2 {
    top: auto;
    bottom: 0;
    -webkit-animation-delay: -1.0s;
    animation-delay: -1.0s;
  }

  @-webkit-keyframes sk-rotate { 100% { -webkit-transform: rotate(360deg) }}
  @keyframes sk-rotate { 100% { transform: rotate(360deg); -webkit-transform: rotate(360deg) }}

  @-webkit-keyframes sk-bounce {
    0%, 100% { -webkit-transform: scale(0.0) }
    50% { -webkit-transform: scale(1.0) }
  }

  @keyframes sk-bounce {
    0%, 100% { 
      transform: scale(0.0);
      -webkit-transform: scale(0.0);
    } 50% { 
      transform: scale(1.0);
      -webkit-transform: scale(1.0);
    }
  }
  .title {
    font-size: 16vmin;
  }
  footer {
    position: fixed;
    bottom: 1vh;
    width: 100%;
    p {
      letter-spacing: -.5px;
      span {
        position: relative;
        left: -5px;
        top: -7.5px;
        a.underline {
          color: inherit;
          text-decoration: none;
          border-bottom: 3px solid #EF6E7E;
          box-shadow: inset 0 -4px 0 #EF6E7E;
          transition: background .15s cubic-bezier(.33,.66,.66,1);
        }
        a.underline:hover {
          background-color: #EF6E7E;
        }
      }
    }
  }
}
</style>
