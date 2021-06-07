<template>
  <div style="padding: 30px">
    <div class="progress-bar">
      <div class="progress-marker">
        <crumb
          class="crumb--font"
          width="200"
          height="60"
          :border-size="4"
          border-color="darkgreen"
          bg-color="green"
          text="this is a test"
        />
      </div>
      <div class="progress-marker" style="left: 188px">
        <crumb
          class="crumb--font"
          width="200"
          height="60"
          :border-size="4"
          border-color="darkgreen"
          bg-color="green"
          text="this is a test"
          text-color="white"
          left-indent
        />
      </div>
      <div class="progress-marker" style="left: 376px">
        <crumb
          class="crumb--font"
          width="200"
          height="60"
          bg-color="lightgray"
          border-color="gray"
          :border-size="4"
          left-indent
        />
      </div>
    </div>
    <div class="progress-bar-footer">
      <crumb
        width="100%"
        height="32"
        border-color="black"
        :border-size="2"
        text="Requestor Progress"
        text-color="white"
        left-indent
      />
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
  font-size: 24px;
  font-family: "Times New Roman", Times, serif;
  font-weight: 700;
}
.progress-bar {
  position: relative;
  height: 60px;
}
.progress-marker {
  position: absolute;
  top: 0;
  left: 0;
}
.progress-bar-footer {
  font-size: 20px;
  margin-top: 5px;
  width: 576px;
  text-align: center;
}
</style>
