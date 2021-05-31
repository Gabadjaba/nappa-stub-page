<template>

  <div class="stub-page">
    <div class="stub-page__container">
      <img class="stub-page__logo" src="@/assets/svg/vandal-logo.svg" alt="vandal-logo">
      <p class="stub-page__text"> Coming Soon </p>
    </div>
  </div>
  <div id="cursor" class="stub-page__cursor"/>

  <svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="800">
    <defs>
      <filter id="goo">
        <feGaussianBlur in="SourceGraphic" stdDeviation="6" result="blur" />
        <feColorMatrix in="blur" mode="matrix" values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 35 -15" result="goo" />
        <feComposite in="SourceGraphic" in2="goo" operator="atop"/>
      </filter>
    </defs>
  </svg>
</template>

<script>
  import cursor from '@/utils/cursor';

  export default {
    name: "Stub",
    mounted() {
      cursor(document.getElementById("cursor"));
    }
  }
</script>

<style>

  svg {
    display: none;
  }

  img {
    pointer-events: none;
  }

  .stub-page {
    cursor: none;
    user-select: none;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 100%;
    background-image: url(~@/assets/svg/vandal-large.svg);
    background-size: cover;
    background-position: center;
  }

  .stub-page__cursor {
    pointer-events: none;
    position: fixed;
    display: block;
    border-radius: 0;
    transform-origin: center center;
    mix-blend-mode: difference;
    top: 0;
    left: 0;
    z-index: 1000;
    filter: url('#goo');
  }

  .stub-page__cursor span {
    position: absolute;
    display: block;
    width: 26px;
    height: 26px;
    border-radius: 20px;
    background-color: white;
    transform-origin: center center;
    transform: translate(-50%, -50%);
  }


  .stub-page__container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .stub-page__logo {
    margin: 16px;
    width: 98%;
    max-width: 680px;
  }

  .stub-page__text {
    text-align: center;
    color: white;
    font-size: 2.250em;
    font-weight: 600;
  }
</style>