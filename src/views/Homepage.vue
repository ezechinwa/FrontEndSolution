<template>
  <div class="home">
    <div class="centertext">
      <div class="contenttext">
        <p class="mtext-light">
          Show me
          <span class="mtext-bold">invoices</span> of
          <span class="mtext-bold">STF Belgium</span>
        </p>
        <p class="mtext-light">
          from
          <span class="mtext-bold">January</span> to
          <span class="mtext-bold">April</span> of
          <span class="mtext-bold">2018</span>
        </p>
      </div>

      <img class="loader" src="@/assets/images/loader.gif" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "../utils/color.scss";

.loader {
  margin-top: 40px;
  width: 150px;
  // height: 120px;
}
.contenttext {
  text-align: center;
}
.mtext-bold {
  font-size: 40px;
  color: $lightboldfont;
}

.mtext-light {
  font-size: 40px;
  color: $lightfont;
}
p {
  margin: 4px;
  font-weight: 200;
}

.centertext {
  display: flex;
  height: 100vh;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  // line-height: 0px;
  margin-top: 5px;
  flex-wrap: wrap;
}
.page {
  position: fixed;
  widows: inherit;
}
</style>

<script>
import "../router/index.js";

export default {
  name: "Home",
  data() {
    return {};
  },
  mounted() {
    var vm = this;

    setTimeout(function() {
      vm.$router.push({ name: "Listings" });
    }, 8000);
  },
  methods: {},
  components: {
    // HelloWorld
  }
};
</script>
