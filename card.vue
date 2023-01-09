<template>
 
  <div id="card">
    
    <div id="title">
      {{ subevent.name }}
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
          <div id="desc"
               :subevent-name="subevent.name"
               :class="[isWindowNarrow ? 'line-clamp-3' : '']">
            <p v-for="lines in subevent.description[0].desc[0]" :key="lines.id">
              {{ lines }}
              <br />
            </p>
          </div>
          <div v-if="isWindowNarrow"
               class="text-blue-500 cursor-pointer more"
               @click="showMore(subevent.name)">
            Read More
          </div>
          <div v-if="isWindowNarrow"
               class="text-blue-500 cursor-pointer less hidden"
               @click="showLess(subevent.name)">
            Read less
          </div>
        </div>
       <!-- <div id="poc">
          <div id="contact">
            <h5 id="contactHead">Contact:</h5>
            <ul>
              <li v-for="contact in subevent.poc" :key="contact.name">
                <span>{{ contact.name }}</span> : {{ contact.contact }}
              </li>
            </ul>
          </div>
        </div> -->
        <div id="col">
        <div id="prize">Prizes worth: {{ subevent.prize }}K</div>

        <div id="buttons">
          <a v-if="subevent.problem_statement"
             id="ps"
             target="_blank"
             :href="subevent.problem_statement">
            <button type="button" class="btn btn--3">
              <span class="btn__text">View Problem Statement</span>
            </button>
          </a>
          <button v-else type="button" class="btn btn--3">
            <span class="btn__text">Problem Statement coming soon!</span>
          </button>
          <div id="btn btn--4">
          <a href="https://dashboard.technex.co.in/register/event"
             class="button">Register for the Event</a>
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
  
    padding: 4px 8px;
    position: relative;
    flex-wrap:nowrap;
    
  }
  
.line-clamp-3 {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
}

.more,
.less {
  font-family: 'poppins', 'Montserrat';
  padding-left: 4px;
  color:black;
}

  #image {
    max-width: 100%;
    height:auto;         
    display: flex;
    flex-direction: column;
    position: relative;
   
  }
  

  #img {
    
    max-width: 100%;
    height: 100%;
    object-fit: fill;
    position: relative;
    top:0;
    bottom:0;
    left:0;
    right:0;
   
    
    bottom: 0px;
    
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
    /*padding: 4px 8px;*/
    margin-top: 100px;
    /*margin-bottom:40px;*/
  }
  
  

  #title {
    background: rgba(89, 218, 255, 0.8);
    font-family: 'a Autobus Omnibus';
    color: white;
    font-weight: 400;
    font-size: 24px;
    line-height: 27px;
    padding:14px;
    
    
  }
#col{
    display:flex;
    flex-direction:row;
}
  #desc {
    font-size: 20px;
    font-weight: 400;
    line-height: normal;
    
    font-family: 'poppins', 'Montserrat';
    padding: 4px 8px;
  }

#contactHead {
  font-family: 'poppins', 'Montserrat';
  font-size: 18px;
}

#contact {
  padding: 5px 10px;
  font-size: 16px;
}

#poc ul {
  list-style: inside;
  font-family: 'poppins', 'Montserrat';
}
#poc {
  display: flex;
  flex-direction: column;
}



  #content {
    width: 100%;
    height:100%;
        
    background: rgba(89, 218, 255, 0.5);
    color: white;
    display: flex;
    flex-direction: row;
    
    justify-content: space-evenly;
  }


  #buttons {
    display: flex;
    position: relative;
    flex-direction: column;
    padding: 4px 8px;
    margin-top: 90px;
    width: 400px;
    max-width: 100%;
    justify-content: center;
    align-items: center;
  }





.btn__text {
  font-size: 14px;
  font-family: 'poppins', 'Montserrat';
  font-weight: 500;
  color: #fff;
}
  .btn--3 {
    background: transparent;
    position: absolute;
    right: 0;
    padding-top: 13px;
    /*margin: 10px;*/
    bottom:60px;
    padding-left:12px;
    padding-right:12px;
    padding-bottom: 13px;
    


    
  }
.btn--3 .btn__text {
  position:relative;
  z-index: 1;
  color: #ff6f6f;
  transition: color 0.3s;
  padding-bottom: 10px;
}
  .button {
    background: transparent;
    position: absolute;
    right: 0;
    /*padding: 14px;*/
    justify-content: center;
    align-items: center;
    text-decoration: none;
    color: white;
    height: 46px;
    font-family: 'poppins', 'Montserrat';
    font-weight: 550;
    /*padding-right: 44px !important;*/
    transition: all 0.1s linear;
    transform: translateZ(0);
    padding: 12px 40px;
    border-radius: 40px;
    background:#ff6f6f;
    margin-right:0px;
    bottom:2px;
  }
  .btn--3::after {
    position: absolute;
    top: calc(100%);
    left: 0;
    display: block;
    height: 2px;
    width: 100%;
    content: '';
    background: #04101C;
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




  #overall {
    display: flex;
    flex-direction: column;
    padding: 14px;
    position: relative;
    width: 100%;
    
    
  }
  #overview{
      position:relative;
      
  }
  @media screen and (max-width: 1120px) {
  #card {
    display: flex;
    flex-direction: column;
    width: 70vw;
  }
  .btn--3 {
    background: transparent;
    position: relative;
   margin-left:120px;
    
  }
  #col{
      flex-direction:column;
  }
  #content{
      flex-direction:column;
      
  }
  #image {
    width: 100%;
    height:auto;
    
  }
  #img,
  #overlay {
    
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
    
  }
  #title {
    padding-bottom:10px;
    padding-left: 20px;
    justify-content:center;
    align-items:center;
    text-align:center;
  }
  #desc {
    font-size: 14px;
    font-weight: normal;
    padding: 2px 4px;
    display: inline-block;
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
    flex-direction: column-reverse;
    align-self: flex-end;
  }
}



@media screen and (max-width: 960px) {
  #card {
    display: flex;
    flex-direction: column;
    width: 70vw;
  }
  #overview{
      
      align-items: center;
      justify-content: center;
      margin-left:160px;
      margin-right:0px;
  }
  #buttons {
    
      justify-content: center;
      align-items: center;
      align-self: center;
    }
   #button
   {  position: absolute;
      justify-content: center;
      align-items: center;
     
   }
   #overall {
    display: flex;
    flex-direction: column;
    padding: 14px;
    position: relative;
    width: 100%;
    padding-right:100px;
   
    
    
  }
  
  .btn--3 {
    background: transparent;
    position: relative;
    justify-content:center;
    align-items:center;
    
  }
  #col{
      flex-direction:column;
  }
  #content{
      flex-direction:column;
      
  }
  #image {
    width: 100%;
    height:auto;
    border-radius: 0px 0px 0px 0px;
  }
  #img,
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
    
  }
  #title {
    padding-bottom:40px;
    padding-left: 20px;
    padding-top:40px;
  }
  #desc {
    font-size: 14px;
    font-weight: normal;
    padding: 2px 4px;
    display: inline-block;
    max-width: 70%;
    text-align:center;
    justify-items: center;
    justify-content: center;
  }
  #contact {
    font-size: 14px;
  }
  #contactHead {
    font-size: 16px;
  }
  #buttons {
    display: flex;
    flex-direction: column-reverse;
    align-self: center;
  }
}

@media screen and (max-width: 470px) {
  #card {
    display: flex;
    flex-direction: column;
    width: 90vw;
  }
}
</style>
