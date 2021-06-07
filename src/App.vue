<template>
  <div style="padding: 30px">
    <div class="offer-progress-bar scrollbar">
      <div class="requestor-progress">
        <div class="markers-container">
          <crumb
            class="crumb--font"
            width="140"
            height="60"
            border-color="#59876a"
            bg-color="#70ad47"
            text="Offer Matrix Uploaded"
          />
          <crumb
            class="crumb--font"
            width="100%"
            height="60"
  
            border-color="#59876a"
            bg-color="#70ad47"
            text="Audience Files Updated"
            text-color="white"
            left-indent
          />
          <crumb
            class="crumb--font"
            width="100%"
            height="60"
            bg-color="#70ad47"
            border-color="#59876a"
            :border-size="2"
            text="Request Files Validated"
            text-color="white"
            left-indent
          />
          <crumb
            class="crumb--font"
            :class="{ 'crumb--not-complete': notComplete }"
            width="100%"
            height="60"
            bg-color="#70ad47"
            border-color="#59876a"
            :border-size="2"
            text="Work Request Submitted"
            text-color="white"
            left-indent
          />               
        </div>
        <crumb
          class="progress-bar-footer"
          width="100%"
          height="20"
          border-color="black"
          bg-color="lightgray"
          text="Requestor"
          text-color="black"
        />        
      </div>
      <div class="offer-delivery-progress">
        <div class="markers-container">
          <crumb
            class="crumb--font crumb--not-complete"
            width="100%"
            height="60"
            bg-color="#70ad47"
            border-color="#59876a"
            :border-size="2"
            text="Work Request Acknowledged"
            text-color="white"
            left-indent
          />      
          <crumb
            class="crumb--font crumb--not-complete"
            width="100%"
            height="60"
            bg-color="#70ad47"
            border-color="#59876a"
            :border-size="2"
            text="Work Request Assigned"
            text-color="white"
            left-indent
          />      
          <crumb
            class="crumb--font crumb--not-complete"
            width="100%"
            height="60"
            bg-color="#70ad47"
            border-color="#59876a"
            :border-size="2"
            text="Work Request Configured"
            text-color="white"
            left-indent
          />      
          <crumb
            class="crumb--font crumb--not-complete"
            width="100%"
            height="60"
            bg-color="#70ad47"
            border-color="#59876a"
            :border-size="2"
            text="Work Request Published"
            text-color="white"
            left-indent
          />  
          <crumb
            class="crumb--font crumb--not-complete"
            width="100%"
            height="60"
            bg-color="#70ad47"
            border-color="#59876a"
            :border-size="2"
            text="Final QA Completed"
            text-color="white"
            left-indent
          />      
          <crumb
            class="crumb--font crumb--not-complete"
            width="100%"
            height="60"
            bg-color="#70ad47"
            border-color="#59876a"
            :border-size="2"
            text="Ready to Go Live"
            text-color="white"
            left-indent
          />                                       
        </div>
        <crumb
          class="progress-bar-footer"
          width="100%"
          height="20"
          border-color="black"
          bg-color="lightgray"
          text="Offer Delivery Team"
          left-indent
          text-color="black"
        />        
      </div>   
    </div>


  </div>
</template>

<script>
import Crumb from "./components/Crumb";

export default {
  name: "App",
  components: {
    Crumb,
  },
  data() {
    return { notComplete: true };
  },
  mounted() {
    setTimeout(() => {
      this.notComplete = false;
    }, 2000);
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.crumb--font {
  font-size: 16px;
  line-height: 16px;
  font-family: Calibri;
  font-weight: 700;
  opacity: 1;
  transition: opacity .75s;
  min-width: 135px;
}
.crumb--not-complete {
  transition: opacity .75s;
  opacity: .4;
}
.offer-progress-bar {
  display: flex;
  overflow-x: auto;
}
.progress-bar-footer{
  font-style: italic;
  font-size: 16px;
  font-weight: 700;
  text-align: center;
}
.markers-container {
  display: flex;
  flex-direction: row;
  margin-bottom: 5px;
}

.scrollbar::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}
.scrollbar::-webkit-scrollbar-track {
  border-radius: 10px;
  background: rgba(0,0,0,0.1);
}
.scrollbar::-webkit-scrollbar-thumb{
  border-radius: 10px;
  background: rgba(0,0,0,0.2);
}
.scrollbar::-webkit-scrollbar-thumb:hover{
  background: rgba(0,0,0,0.4);
}
.scrollbar::-webkit-scrollbar-thumb:active{
  background: rgba(0,0,0,.9);
}
</style>
