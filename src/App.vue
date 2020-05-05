<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link>|
      <router-link to="/about">About</router-link>
    </div>-->
    <!-- enter-active-class="animated fadeOutUp" leave-active-class="animated fadeOutUp" -->
    <transition name="fadeOutUp" leave-active-class="animated fadeOutUp">
      <router-view />
    </transition>

    <custom-cursor
      :targets="['img', 'a', 'button', 'your-hover-class']"
      :circleColor="'#cfcfcf'"
      :circleColorHover="'#2f2f2f'"
      :dotColor="'#F7FAFF'"
      :dotColorHover="'#F7FAFF'"
      :hoverSize="1.8"
    ></custom-cursor>
  </div>
</template>

<script>
import "animate.css";
import CustomCursor from "../src/components/CustomCursor.vue";

export default {
  name: "App",
  components: { CustomCursor }
};
</script>

<style lang="scss">
@import "./utils/general.scss";
@import "./utils/color.scss";

html,
body {
  max-width: 100%;
  overflow: hidden;

  cursor: none;
  margin: 0px;
  padding: 0px;
  background: linear-gradient(
      to left top,
      $bgbottomrightrgba 0% /*bottom-right color*/,
      $bgtopleftrgba 400% /*top-left color*/
    ),
    linear-gradient(rgba(0, 0, 0, 1), rgba(0, 0, 0, 1));
  height: 100%;
  max-height: 100%;
  font-family: "Work Sans", sans-serif;
}
</style>
