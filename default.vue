
<template>
  <main>
    <PageLoader />
    <header>
      <div class="hidden lg:block"><Navbar /></div>
      <div class="lg:hidden"><NavbarMobile /></div>
    </header>
    <bgGrid class="gridBg" />
    <Nuxt keep-alive />
    <div v-if="visible">
      <a id="leftBtn" class="StickyBtn" href="#" target
        >Catch All Latest News Here!</a
      >
      <a id="rightBtn" class="StickyBtn" href="#" target>Register Now</a>
    </div>
    <footer>
      <Footer @visibility="visibility" />
    </footer>
  </main>
</template>

<script>
import bgGrid from '../components/Home/bgGrid.vue'
import NavbarMobile from '../components/NavbarMobile.vue'
import Navbar from '../components/Navbar.vue'
import Footer from '../components/Footer.vue'
import PageLoader from '../components/Event/PageLoader.vue'

export default {
  components: { Navbar, NavbarMobile, Footer, bgGrid ,PageLoader},
  data() {
    return {
      visible: true,
    }
  },
  methods: {
     visibility(value)
     {
        this.visible=!value
     }
  }
}

</script>

<style>
body {
  background-color: #1d1d1d;
  /* overflow:hidden; */
}
body,
html {
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 0;
  padding: 0;
  background-color: #04101C;
  font-family: 'Lato';
font-style: normal;
font-weight: 400;
}

.grid{
  position:fixed;
  z-index: inherit;
}

/* Scrollbar */
::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px #163a4a;
  border-radius: 12px;
  background-color: #fff;
}

::-webkit-scrollbar {
  width: 5px;
  background-color: #fff;
}

::-webkit-scrollbar-thumb {
  border-radius: 12px;
  -webkit-box-shadow: inset 0 0 6px #163a4a;
  background-color: #444;
}

.StickyBtn {
  position: fixed;
  bottom: 30px;
  font-size: 20px;
  background: url('/button_bg.webp') no-repeat center/cover;
  color: white;
  z-index: 10;
  width: 270px;
  height: 72px;
  font-family: 'aAutobusOmnibus', 'Montserrat';
  text-align: center;
  display: grid;
  align-items: center;
}

#leftBtn {
  left: 0px;
  border-radius: 0px 15px 15px 0px;
}

#rightBtn {
  right: 0px;
  border-radius: 15px 0px 0px 15px;
}

@media only screen and (max-width: 800px) {
  .StickyBtn {
    width: 170px;
    height: 45px;
    font-size: 12px;
  }
}

@media only screen and (max-width: 425px) {
  .StickyBtn {
    width: 100px;
    height: 30px;
    font-size: 8px;
  }
  #leftBtn {
    left: 0px;
    border-radius: 0px 6px 6px 0px;
  }

  #rightBtn {
    right: 0px;
    border-radius: 6px 0px 0px 6px;
  }
}
</style>
