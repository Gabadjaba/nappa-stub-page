<template>
  <Stub/>
</template>

<script>
import Stub from './components/Stub/index'

export default {
  name: 'App',
  components: {
    Stub
  }
}
</script>

<style>

  @font-face {
    font-family: "EB Garamond";
    src: local("EB Garamond"),
    url(./assets/fonts/EBGaramond-Regular.ttf) format("truetype");
  }

  * {
    margin: 0;
    padding: 0;
  }

  #app {
    font-family: 'EB Garamond', serif;
    font-size: 16px;
    background-color: #F37668;

    height: 100vh;
    width: 100vw;
  }
</style>
