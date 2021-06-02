<template>
  <div class="stub-page" ref="stubPage">
    <div class="stub-page__container">
      <vandal-logo class="stub-page__logo"/>
      <p class="stub-page__text"> Coming Soon </p>
    </div>
  </div>
  <div class="stub-page__second" ref="stubPageSecond">
    <div class="stub-page__container">
      <vandal-logo class="stub-page__logo"/>
      <p class="stub-page__text"> Coming Soon </p>
    </div>
  </div>
  <div class="stub-page__circle" ref="stubPageCircle"></div>
</template>

<script>
  import Kinet from 'kinet'
  import VandalLogo from '@/assets/svg/vandal-logo.svg'

  export default {
    name: "Stub",
    components: {
      VandalLogo
    },
    methods: {
      cursorInit(){
        // create instance of kinet with custom settings
        const kinet = new Kinet({
          acceleration: 0.03,
          friction: 0.10,
          names: ["x", "y"]
        })

        // const cursor = this.$refs.cursor
        const stubPageSecond = this.$refs.stubPageSecond
        const stubPageCircle = this.$refs.stubPageCircle

        // set handler on kinet tick event
        kinet.on('tick', function(instances) {
          stubPageSecond.style.clipPath = `circle(60px at ${instances.x.current}px ${instances.y.current}px)`
          stubPageCircle.style.transform = `translate3d(${ (instances.x.current - window.innerWidth/2) }px, ${ (instances.y.current - window.innerHeight/2) }px, 0)`
        })

        // call kinet animate method on mousemove
        document.addEventListener('mousemove', function (event) {
          kinet.animate('x', event.clientX)
          kinet.animate('y', event.clientY)
        })
      }
    },
    mounted() {
      this.cursorInit()
    }
  }
</script>

<style>

  .stub-page, .stub-page__second {
    position: absolute;
    touch-action: none;
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
    z-index: 0;
    background-image: url(~@/assets/png/vandal-bg.png);
    background-size: cover;
    background-position: center;
  }

  .stub-page .stub-page__logo {
    fill: #FFFFFF;
  }

  .stub-page .stub-page__text {
    color: #FFFFFF;
  }

  .stub-page__second {
    clip-path: circle(0px at 0px 0px);
    filter: brightness(0.5) sepia(1) hue-rotate(-70deg) saturate(5);
    z-index: 2;
  }

  .stub-page__second .stub-page__logo {
    fill: blue;
  }

  .stub-page__second .stub-page__text {
    color: blue;
  }

  .stub-page__container {
    width: 100%;
    max-width: 681px;
    padding: 2vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .stub-page__text {
    text-align: center;
    font-size: 2.250em;
    font-weight: 600;
  }

  .stub-page__circle {
    --size: 15px;
    top: 50%;
    left: 50%;
    width: var(--size);
    height: var(--size);
    position: fixed;
  }
</style>