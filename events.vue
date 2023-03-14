<template>
  <div class="h-full min-h-screen w-full pt-25 md:pt-20">
    <Header :title="'Events'" />
    <p class="sub-heading">* Some events have free participation for Round 1</p>
    <section id="eventsNav" class="pt-20 md:pt-25">
      <section id="eventsBtn">
        <div
          v-for="(event, index) in events"
          :key="index"
          class="badge"
          :class="activeEvent == index ? 'activeEvent' : ''"
          @click="eventLoad(index)"
        >
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          {{ event.parent }}
        </div>
      </section>
    </section>
    <EventTime-line v-if="isDataFetched" :event="events[activeEvent]" />
    <div class="head">
      <u
        ><h2 id="tc">
          <a
            href="https://drive.google.com/file/d/1NZvu6KchKiePN4FPSUcp1aDT0BFRpoe4/view?usp=drivesdk"
            target="_blank"
            class="relative z-1"
          ></a></h2
      ></u>
    </div>
    <br /><br />
  </div>
</template>

<script>
export default {
  data() {
    return {
      events: [],
      activeEvent: 0,
      isDataFetched: false,
    }
  },
  async fetch() {
    const fetchedData = await this.$content('events').fetch()
    this.isDataFetched = true
    this.events = fetchedData
  },
  mounted() {
    const myNav = document.getElementById('navbar')
    window.onscroll = function () {
      'use strict'
      if (window.pageYOffset >= 50) {
        myNav.classList.add('nav-colored')
        myNav.classList.remove('nav-transparent')
      } else {
        myNav.classList.add('nav-transparent')
        myNav.classList.remove('nav-colored')
      }
    }
  },
  methods: {
    eventLoad(index) {
      this.activeEvent = index
    },
  },
}
</script>

<style scoped>
.head #tc {
  color: aliceblue;
  text-align: center;
  font-size: 22px;
  font-family: 'Lato';
}

.head a:hover {
  color: #59daff;
}

.sub-heading {
  margin-left: 20%;
  margin-right: 20%;
  font-weight: bold;
  font-size: 20px;
  text-align: center;
  color: white;
  margin-top: 30px;
  position: relative;
  z-index: 1;
}

#eventsBtn {
  padding: 1.5rem 1rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.badge {
  cursor: pointer;
  position: relative;
  padding: 10px 20px;
  margin: 10px;
  display: inline-flex;
  color: white;
  text-align: center;
  font-family: 'Lato', 'Montserrat';
  letter-spacing: 1.2px;
  text-decoration: none;
  font-size: 20px;
  overflow: hidden;
  transition: 0.2s;
}
.badge:hover {
  color: #fff;
  background: #59daff;
  box-shadow: 0 0 8px #59daff, 0 0 30px #59daff, 0 0 65px #59daff;
  transition-delay: 1s;
  border-radius: 12px 12px 12px 12px;
}
.badge span {
  position: absolute;
  display: block;
}
.badge span:nth-child(1) {
  top: 0;
  left: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #59daff);
  border-radius: 12px 12px 12px 12px;
}
.badge:hover span:nth-child(1) {
  left: 100%;
  transition: 1s;
  border-radius: 12px 12px 12px 12px;
}
.badge span:nth-child(3) {
  bottom: 0;
  right: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(270deg, transparent, #59daff);
  border-radius: 12px 12px 12px 12px;
}
.badge:hover span:nth-child(3) {
  right: 100%;
  transition: 1s;
  transition-delay: 0.5s;
  border-radius: 12px 12px 12px 12px;
}
.badge span:nth-child(2) {
  top: -100%;
  right: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(180deg, transparent, #59daff);
  border-radius: 12px 12px 12px 12px;
}
.badge:hover span:nth-child(2) {
  top: 100%;
  transition: 1s;
  transition-delay: 0.25s;
  border-radius: 12px 12px 12px 12px;
}
.badge span:nth-child(4) {
  bottom: -100%;
  left: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(360deg, transparent, #59daff);
  border-radius: 12px 12px 12px 12px;
}
.badge:hover span:nth-child(4) {
  bottom: 100%;
  transition: 1s;
  transition-delay: 0.75s;
  border-radius: 12px 12px 12px 12px;
}
.activeEvent {
  background-color: #59daff;
  color: black;
  border-radius: 12px 12px 12px 12px;
}

@media only screen and (max-width: 775px) {
  .head #title {
    font-size: 10px;
  }
  .head #tc {
    margin-left: 16px;
    font-size: 25px;
  }
  #eventsBtn {
    padding: 1rem 1rem;
  }
  .badge {
    padding: 8px 16px;
    font-size: 16px;
  }
  .icon {
    width: 45px;
  }
}
@media only screen and (max-width: 775px) {
  .head #tc {
    font-size: 20px;
  }
}

@media only screen and (max-width: 700px) {
  .sub-heading {
    font-size: 16px;
  }
}
</style>
