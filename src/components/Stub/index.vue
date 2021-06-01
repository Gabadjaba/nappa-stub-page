<template>
  <div class="stub-page" ref="stubPage">
    <div class="stub-page__container">
      <img class="stub-page__logo" src="@/assets/svg/vandal-logo.svg" alt="vandal-logo">
      <p class="stub-page__text"> Coming Soon </p>
    </div>
  </div>
  <div
      class="stub-page__cursor"
      ref="cursor">
  </div>
</template>

<script>
  import Kinet from 'kinet';

  export default {
    name: "Stub",
    methods: {
      cursorInit(){
        // create instance of kinet with custom settings
        const kinet = new Kinet({
          acceleration: 0.06,
          friction: 0.20,
          names: ["x", "y"],
        });

        const cursor = this.$refs.cursor

        // set handler on kinet tick event
        kinet.on('tick', function(instances) {
          cursor.style.transform = `translate3d(${ (instances.x.current) }px, ${ (instances.y.current) }px, 0) rotateX(${ (instances.x.velocity/2) }deg) rotateY(${ (instances.y.velocity/2) }deg)`;
        });

        // call kinet animate method on mousemove
        document.addEventListener('mousemove', function (event) {
          kinet.animate('x', event.clientX - window.innerWidth/2);
          kinet.animate('y', event.clientY - window.innerHeight/2);
        });
      }
    },
    mounted() {
      this.cursorInit()
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
    overflow: hidden;
    height: 100vh;
    width: 100vw;
    min-height: 420px;
    user-select: none;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #F37668;
    background-image: url(~@/assets/svg/vandal-large.svg);
    background-size: cover;
    background-position: center;
  }

  .stub-page__cursor {
    --size: 120px;

    width: var(--size);
    height: var(--size);
    background: white;
    border-radius: 50%;
    position: fixed;
    top: 50%;
    left: 50%;
    margin: calc(var(--size) / 2 - var(--size) / 2 * 2) 0 0 calc(var(--size) / 2 - var(--size) / 2 * 2);
    pointer-events: none;
    mix-blend-mode: difference;
    z-index: 10;
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