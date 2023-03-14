<template>
  <div id="card">
    <div id="title">
      {{ subevent.name }}
      <div id="circle">
        <img src="/speakers/speakercardcircle.svg" class="test" />
      </div>
    </div>

    <div id="content">
      <div id="image">
        <img id="img" :src="subevent.thumbnail" alt="subEvent-image" />
        <div id="overlay">
          <div v-if="subevent.sponsor" id="logo">
            <img id="logoimg" :src="subevent.sponsor" alt="sponsorLogo" />
          </div>
        </div>
      </div>
      <div id="overall">
        <div id="overview">
          <div
            id="desc"
            :subevent-name="subevent.name"
            :class="[isWindowNarrow ? 'line-clamp-3' : '']"
          >
            <p v-for="lines in subevent.description[0].desc[0]" :key="lines.id">
              {{ lines }}
              <br />
            </p>
          </div>
          <div
            v-if="isWindowNarrow"
            class="text-blue-500 cursor-pointer more"
            @click="showMore(subevent.name)"
          >
            Read More
          </div>
          <div
            v-if="isWindowNarrow"
            class="text-blue-500 cursor-pointer less hidden"
            @click="showLess(subevent.name)"
          >
            Read less
          </div>
        </div>
        <div v-if="subevent.poc" id="poc">
          <div id="contact">
            <h5 id="contactHead">Contact:</h5>
            <ul>
              <li v-for="contact in subevent.poc" :key="contact.name">
                <span>{{ contact.name }}</span> : {{ contact.contact }}
              </li>
            </ul>
          </div>
        </div>
        <div v-if="subevent.prerequisite" id="poc">
          {{ subevent.prerequisite }}
        </div>
        <div id="col">
          <div v-if="subevent.prize" id="prize"></div>
          <div v-if="subevent.sessions" id="prize">
            {{ convertDate(subevent.sessions[0].start) }}<br />
            <div id="venue">
              {{ subevent.sessions[0].venue }}
            </div>
          </div>

          <div v-if="subevent.prize" id="buttons">
            <a
              v-if="subevent.problem_statement"
              id="ps"
              target="_blank"
              :href="subevent.problem_statement"
            >
              <button type="button" class="btn btn--3">
                <span class="btn__text">View Problem Statement</span>
              </button>
            </a>
            <button v-else type="button" class="btn btn--3">
              <span class="btn__text">Problem Statement coming soon!</span>
            </button>

            <div id="buttons-2">
              <div v-if="subevent.register_UnStop" class="btn btn-1" >
                <a
                  :href="subevent.register_UnStop"
                  class="button-custom"
                  >Explore
                </a>
              </div>
              <div class="btn btn-2">
                <a
                  href="https://dashboard.technex.co.in/register/event"
                  class="button-custom"
                  >Register for the Event
                </a>
              </div>
              
            </div>
          </div>
          <div v-if="subevent.sessions" id="buttons">
            <a
              v-if="subevent.content"
              id="ps"
              target="_blank"
              :href="subevent.content"
            >
              <button type="button" class="btn btn--3">
                <span class="btn__text">Content for the Workshop</span>
              </button>
            </a>
            <div id="btn btn--4">
              <a
                href="https://dashboard.technex.co.in/register/event"
                class="button"
                >Register for the Event
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    subevent: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      isWindowNarrow: false,
      isreadmore: true,
    }
  },
  mounted() {
    window.addEventListener('resize', this.setWindowNarrow)
  },
  methods: {
    convertDate(date) {
      return new Date(date).toLocaleString('en-IN', {
        month: 'short',
        day: '2-digit',
        hour: '2-digit',
        minute: '2-digit',
        hour12: true,
      })
    },
    setWindowNarrow() {
      if (window.innerWidth < 960) {
        this.isWindowNarrow = true
      } else this.isWindowNarrow = false
    },
    showMore(eventName) {
      const desc = document.querySelector('[subevent-name="' + eventName + '"]')
      const readMoreButton = desc.nextElementSibling
      const readLessButton = desc.nextElementSibling.nextElementSibling
      readLessButton.classList.toggle('hidden')
      readMoreButton.classList.toggle('hidden')
      desc.classList.remove('line-clamp-3')
    },
    showLess(eventName) {
      const desc = document.querySelector('[subevent-name="' + eventName + '"]')
      const readLessButton = desc.nextElementSibling.nextElementSibling
      const readMoreButton = desc.nextElementSibling
      readLessButton.classList.toggle('hidden')
      readMoreButton.classList.toggle('hidden')
      desc.classList.add('line-clamp-3')
    },
  },
}
</script>

<style scoped>
#card {
  max-width: 75vw;
  z-index: 4;
  border: none;
  display: flex;
  flex-direction: column;
  margin: 40px 0px;
  padding: 4px 8px;
  position: relative;
  flex-wrap: nowrap;
  z-index: 0;
}

.line-clamp-3 {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
}

.more,
.less {
  font-family: 'Lato', 'Montserrat';
  padding-left: 4px;
  color: black;
}

#image {
  max-width: 100%;
  height: auto;
  display: flex;
  flex-direction: column;
  position: relative;
}

#img {
  max-width: 100%;
  height: 100%;
  object-fit: fill;
  position: relative;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  bottom: 0px;
  border-radius: 0px 0px 0px 12px;
}

#logo {
  width: 30%;
  margin: 6px 20px;
}

#logoimg {
  width: 100%;
  height: 100%;
  border-radius: 4px;
  object-fit: contain;
}

#prize {
  font-weight: 900;
  font-size: 24px;
  line-height: 24px;
  padding: 4px 8px;
  margin-top: 100px;
  margin-bottom: 40px;
  width: 75%;
}

#title {
  background: rgba(89, 218, 255, 0.8);
  font-family: 'aAutobusOmnibus';
  color: white;
  font-weight: 400;
  line-height: 27px;
  padding: 14px;
  font-size: 30px;
  border-radius: 12px 12px 0px 0px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

#col {
  display: flex;
  flex-direction: row;
}

#desc {
  font-size: 20px;
  font-weight: 400;
  line-height: normal;
  font-family: 'Lato', 'Montserrat';
  padding: 4px 8px;
}

#contactHead {
  font-family: 'Lato', 'Montserrat';
  font-size: 18px;
}

#contact {
  padding: 5px 10px;
  font-size: 16px;
}

#poc ul {
  list-style: inside;
  font-family: 'Lato', 'Montserrat';
}

#poc {
  display: flex;
  flex-direction: column;
  padding: 4px 8px;
  margin-top: 10px;
}

#venue {
  margin-top: 5px;
}

#content {
  width: 100%;
  height: 100%;
  background: rgba(89, 218, 255, 0.5);
  color: white;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  border-radius: 0px 0px 12px 12px;
}

#buttons {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 4px 8px;
  margin-top: 30px;
  width: 400px;
  max-width: 100%;
  justify-content: center;
  align-items: center;
}

#buttons-2{
  display: flex;
  padding: 4px 8px;
  margin-top: 30px;
  width: 400px;
  max-width: 100%;
  align-items: center;
  justify-content: flex-end;
}

.btn-1{
  margin-right: 15px;
}

.btn__text {
  font-size: 14px;
  font-family: 'Lato', 'Montserrat';
  font-weight: 500;
  color: #fff;
}

.btn--3 {
  background: transparent;
  position: absolute;
  right: 0;
  padding: 14px;
  margin: 10px;
  bottom: 100px;
}


.btn--3 .btn__text {
  position: relative;
  z-index: 1;
  color: #04101c;
  transition: color 0.3s;
}

.button {
  background: transparent;
  position: absolute;
  right: 0;
  padding: 14px;
  justify-content: center;
  align-items: center;
  text-decoration: none;
  color: white;
  height: 46px;
  font-family: 'Lato', 'Montserrat';
  font-weight: 550;

  transition: all 0.1s linear;
  transform: translateZ(0);
  padding: 12px 40px;
  border-radius: 40px;
  background: #04101c;
  margin-bottom: 40px;
}

.button-custom
{
  text-decoration: none;
  color: white;
  font-family: 'Lato', 'Montserrat';
  font-weight: 550;
  transition: all 0.1s linear;
  /* transform: translateZ(0); */
  padding: 12px 20px;
  border-radius: 40px;
  background: #04101c;
  margin: 40px 0; 
}

.btn--3::after {
  position: absolute;
  top: calc(100%);
  left: 0;
  display: block;
  height: 2px;
  width: 100%;
  content: '';
  background: #04101c;
  transition: all 0.3s;
}

.btn--3:hover::after {
  border-radius: 40px;
  top: 0;
  height: 100%;
}

.btn--3:hover .btn__text {
  color: #fff;
}

#overlay {
  position: absolute;
  border-radius: 0px 0px 0px 12px;
  display: flex;
  justify-content: flex-end;
  flex-direction: column;
  left: 0px;
  bottom: 0px;
  z-index: 4;
  width: 100%;
  height: 35%;
  color: aliceblue;
  background: linear-gradient(180deg, rgba(0, 0, 0, 0) 0%, #000000 100%);
  backdrop-filter: blur(1px);
  -webkit-backdrop-filter: blur(2px);
}

#overall {
  display: flex;
  flex-direction: column;
  padding: 14px;
  position: relative;
  width: 100%;
}

#overview {
  position: relative;
  text-align: left;
}

@media screen and (max-width: 1120px) {
  #card {
    display: flex;
    flex-direction: column;
    width: 70vw;
  }

  .button {
    position: relative;
  }

  .btn--3 {
    background: transparent;
    position: relative;
    justify-content: center;
    align-items: center;
    bottom: 20px;
    margin: 0px;
  }

  #col {
    flex-direction: column;
  }

  #content {
    flex-direction: column;
  }

  #image {
    width: 100%;
    height: auto;
  }

  #img {
    border-radius: 0px 0px 0px 0px;
  }

  #overlay {
    border-radius: 0px 0px 0px 0px;
  }

  #content {
    width: 100%;
    height: 60%;
    border-radius: 0px 0px 12px 12px;
  }

  #logo {
    width: 25%;
    margin-bottom: 2px;
  }

  #prize {
    margin-top: 10px;
    margin-bottom: 0px;
    font-size: 20px;
  }

  #title {
    padding-bottom: 10px;
    padding-left: 20px;

    text-align: left;
  }

  #desc {
    font-size: 14px;
    font-weight: normal;
    padding: 2px 4px;

    max-width: 100%;
  }

  #contact {
    font-size: 14px;
  }

  #contactHead {
    font-size: 16px;
  }

  #buttons {
    display: flex;
    flex-direction: column;
    align-self: flex-end;
    margin-top: 30px;
  }
}

@media screen and (max-width: 960px) {
  #buttons {
    justify-content: center;
    align-items: center;
    align-self: center;
  }
  #buttons-2{
    justify-content: center;
    align-items: center;
  }

  .button {
    position: relative;
  }
  #title {
    font-size: 20px;
  }
}

@media screen and (max-width: 470px) {
  .btn-1{
    margin-bottom: 35px;
  }
  #card {
    display: flex;
    flex-direction: column;
    width: 90vw;
  }
  #buttons-2{
    flex-direction: column;
  }
  .button {
    font-size: 15px;
    padding: 15px;
  }

  #prize {
    font-size: 16px;
  }

  .btn--3 .btn__text {
    font-size: 14px;
  }

  .btn--3 {
    padding: 3px;
  }
  #title {
    font-size: 15px;
  }
}

@media screen and (max-width: 360px) {
  #prize {
    font-size: 15px;
  }
  .button-custom{
    font-weight: 400;
    font-size: x-small;
    padding: 12px 14px;
  }

}
</style>