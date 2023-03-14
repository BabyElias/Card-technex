<template>
  <div class="top">
    <div id="head" class="relative z-1">
      <h3 id="parentDesc">
        {{ event.desc }}
      </h3>
    </div>
    <section id="events">
      <div
        v-for="(subEvent, index) in event.events"
        :key="index"
        ref="sections"
        class="card"
      >
        <EventCard :subevent="subEvent" />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  props: {
    event: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style scoped>
.top {
  z-index: 1;
}
#parentDesc {
  color: #fff;
  font-family: 'Lato', 'Montserrat';
  width: 42vw;
  margin: 20px auto;
  font-size: 16px;
  z-index: 1;
}

#head {
  text-align: center;
  z-index: 1;
}
#events {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
@media only screen and (max-width: 775px) {
  #parentDesc {
    width: 60vw;
    margin: 15px auto;
    font-size: 14px;
  }
}
@media only screen and (max-width: 450px) {
  #parentDesc {
    width: 70vw;
  }
}
</style>
