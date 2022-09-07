<template>
    <div class="body">
        <div class="background"></div>
        <SignUp class="form" />
    </div>
</template>

<script>
import SignUp from "./components/signUp.vue";



export default {
    name: "App",
    components: { SignUp }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0;
}
body {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        height: 100%;
    }
* {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
.body {
        display: grid;
        grid-template-columns: 2fr 3fr;
    }
.background {
        background-image: url(./assets/greg-rakozy-oMpAz-DN-9I-unsplash.jpg);
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
    }

@media(max-width: 991px) {
    .body {
        grid-template-columns: 1fr;
    }
    .background {
        display: none;
    }
}


</style>
