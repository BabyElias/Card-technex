<template>
    <div class="page-loader" v-if="!isloaded">
     
    </div> 
  </template>
  
  <script>
    export default{
      data: () => {
        return {
          isloaded: false
        }
      },
      mounted() {
        document.onreadystatechange = () => {
          if (document.readyState === "complete") { 
            this.isloaded = true;
          } 
        }
      },
    }
  </script>
  
  <style lang="css" scoped>
   
  
    .page-loader {
      display: flex;
      justify-content: center;
      align-items: center;
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background-image:url('Technex_Loader_MOV_AdobeExpress.gif'); background-repeat:no-repeat;
      z-index: 999;
    }
  
    
  
    
  </style>
