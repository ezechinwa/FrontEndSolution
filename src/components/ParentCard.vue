<template>
  <div :style="{ transform: transformString }">
    <div :class="{arrangeview: !showdetails, arrangeviewshowdetails: showdetails}">
      <transition enter-active-class="animated fadeInUp" leave-active-class="animated fadeInUp">
        <!-- <h1>{{showdetails}}</h1> -->
        <div :class="{cardholder:!showdetails , carddetails: showdetails} " v-if="showtitle">
          <div class="custom-card" :style="{width: cardwidth+ 'px'} ">
            <div class="custom_card_title mb-40">
              <img class="arrow" src="@/assets/images/logo-510.png" />
              <p class="rounded">Unpaid</p>
            </div>

            <div class="custom_card_spacer">
              <div class="custom_card_v-title-start-group">
                <p class="headertext">invoice</p>
                <p class="invoicenumber">{{invoicenumber}}</p>
              </div>

              <div class="custom_card_v-title-group">
                <p class="headertext">Total amount</p>
                <p class="invoicenumber">{{price}}</p>
              </div>
            </div>

            <div class="custom_card_details_spacer">
              <div class="custom_card_v-details-start-group">
                <p class="headertext">Buyer Name</p>
                <p class="mtext-bold">{{buyername}}</p>
              </div>

              <div class="custom_card_v-details-group">
                <p class="headertext">Seller Name</p>
                <p class="mtext-bold">{{sellername}}</p>
              </div>
            </div>

            <div class="custom_card_details_spacer">
              <div class="custom_card_v-details-start-group">
                <p class="headertext">Started</p>
                <p class="mtext-bold">{{date}}</p>
              </div>

              <div class="custom_card_v-details-group">
                <p class="headertext">Blockchain Address</p>
                <p class="mtext-bold">{{address}}</p>
              </div>
            </div>
          </div>
        </div>
      </transition>

      <transition enter-active-class="animated fadeIn">
        <div class="extradetails" v-if="showdetails">
          <div class="custom-card">
            <div class="custom_card_spacer">
              <div class="custom_card_v-title-start-group">
                <p class="invoicenumber">Buyer</p>
              </div>
            </div>

            <div class="details_description">
              <p class="seller-text">STF France</p>
              <p class="seller-text">Des Benjions, Rue 2, Saint-Denis</p>
              <p class="seller-text">1202 RE, Reunion</p>
            </div>

            <hr class="ruler" />

            <div class="custom_card_details_extra_spacer">
              <div class="custom_card_v-details-start-group">
                <p class="seller-text">Code</p>
                <p class="seller-text">Operating Name</p>
                <p class="seller-text">Function</p>
                <p class="seller-text">Trade Registered Number</p>
                <p class="seller-text">VAT Number</p>
                <p class="seller-text">IBAN Number</p>
                <p class="seller-text">BIC Code</p>
              </div>
              <div class="custom_card_v-details-group">
                <p class="seller-text">STFF</p>
                <p class="seller-text">STF France</p>
                <p class="seller-text">Local Operations,Manufacturing,Sales,Marketing</p>
                <p class="seller-text">004101534</p>
                <p class="seller-text">1101317918C49</p>
                <p class="seller-text">RE11NGB4254456990</p>
                <p class="seller-text">INGBRASC</p>
              </div>
            </div>
          </div>

          <div class="custom-card">
            <div class="custom_card_spacer">
              <div class="custom_card_v-title-start-group">
                <p class="invoicenumber">Seller</p>
              </div>
            </div>

            <div class="details_description">
              <p class="seller-text">STF Belgium</p>
              <p class="seller-text">Rue Condorcet 163, Moe</p>
              <p class="seller-text">1264 BE Belgium</p>
            </div>

            <hr class="ruler" />

            <div class="custom_card_details_spacer">
              <div class="custom_card_v-details-start-group">
                <p class="seller-text">Code</p>
                <p class="seller-text">Operating Name</p>
                <p class="seller-text">Function</p>
                <p class="seller-text">Trade Registered Number</p>
                <p class="seller-text">VAT Number</p>
                <p class="seller-text">IBAN Number</p>
                <p class="seller-text">BIC Code</p>
              </div>
              <div class="custom_card_v-details-group">
                <p class="seller-text">STFB</p>
                <p class="seller-text">STF Belgium</p>
                <p class="seller-text">Local Operations, Manufacturing,Sales,Marketing</p>
                <p class="seller-text">190529485</p>
                <p class="seller-text">1625358102C54</p>
                <p class="seller-text">BE19INGB1165807110</p>
                <p class="seller-text">INGBFR1B</p>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import interact from "interactjs";

export default {
  name: "ParentCard",
  props: [
    "invoicenumber",
    "price",
    "buyername",
    "sellername",
    "date",
    "address",
    "showdetailsperent"
  ],
  data() {
    return {
      showtitle: false,
      cardwidth: 700,
      showdetails: false,
      interactPosition: {
        x: 0,
        y: 0,
        rotation: 0
      }
    };
  },
  mounted() {
    var vm = this;
    vm.showtitle = true;

    const element = this.$refs.interactElement;
    interact(element).draggable({
      onmove: event => {
        const x = this.interactPosition.x + event.dx;
        const y = this.interactPosition.y + event.dy;
        this.interactSetPosition({ x, y });
      },
      onend: () => {
        this.resetCardPosition();
      }
    });
  },
  computed: {
    transformString() {
      const { x, y } = this.interactPosition;
      return `translate3D(${x}px, ${y}px, 0)`;
    }
  },
  watch: {
    showdetailsperent: function(val) {
      console.log("show details :" + val);

      this.showdetails = val;
      if (this.showcarddetails) {
        this.cardwidth = 700;
      } else {
        this.cardwidth = 500;
      }
    }
  },
  methods: {
    interactSetPosition(coordinates) {
      const { x = 0, y = 0 } = coordinates;
      this.interactPosition = { x, y };
    },
    resetCardPosition() {
      this.interactSetPosition({ x: 0, y: 0 });
    },
    showcarddetails() {
      this.showdetails = !this.showdetails;
    }
  },
  components: {
    // HelloWorld
    // ParentCard
  }
};
</script>


<style lang="scss" scoped>
@import "../utils/color.scss";
@import "../utils/dimensions.scss";

p {
  font-weight: 200;
}

.walletlogo {
  //   border: 1px solid red;
  position: absolute;
  bottom: 50px;
  right: 50px;
  background-color: $lightblue;
  border-radius: 50px;
  padding: 5px;
  color: white;
}
.arrangeview {
  display: flex;
  // background: chartreuse;
  justify-content: center;
  align-items: center;
}
.arrangeviewshowdetails {
  display: flex;
  // background: chartreuse;
  justify-content: flex-start;
  align-items: center;
  overflow-x: auto;
  white-space: nowrap;

  -ms-overflow-style: none; /* Internet Explorer 10+ */
  scrollbar-width: none;
}
.arrangeviewshowdetails::-webkit-scrollbar {
  display: none;
}

.extradetails {
  // width: 1500px;
  display: flex;
  justify-content: space-evenly;
  border: 30px sold red;
  // background: chartreuse;
  margin-left: 10px;
  margin-right: 10px;
}
.headertext {
  color: $lightfont;
}
.content {
  margin: 20px;
  height: 100vh;
  //   border: 1px solid red;
}
.header {
  display: flex;
  align-items: center;
  margin-top: 20px;
}

.cardholder {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 80vh;
}

.carddetails {
  display: flex;
  align-items: center;
  // justify-content: center;
  height: 80vh;
}

.arrow {
  height: 35px;
  margin-right: 5px;
}
.mtext-bold {
  font-size: 18px;
  color: $lightboldfont;
}
.seller-text {
  font-size: 11px;
  color: $lightboldfont;
}
.mtext-light {
  font-size: 18px;
  color: $lightfont;
}

.custom-card {
  background-color: $white;
  width: 500px;
  height: 400px;
  padding: 20px;
  border-radius: 10px;
  margin-left: 40px;
}

.custom_card_title {
  display: flex;
  justify-content: space-between;
  margin: 20px;
  align-items: center;
  //   border: 1px solid red;
}

.custom_card_spacer {
  display: flex;
  justify-content: space-between;
  margin-left: 20px;
  margin-right: 20px;
  align-items: center;
  //   border: 1px solid red;
}

.details_description {
  margin-left: 20px;
  margin-right: 20px;
  line-height: 1;
  font-size: 12px;
}

.ruler {
  // margin-left: 20px;
  margin: 20px;
  // width: 100%;
  // height: 0.1px;
  border: 0.1px solid $lightfont;
}
.custom_card_details_spacer {
  display: flex;
  //   justify-content: space-evenly;
  margin-left: 20px;
  margin-right: 20px;
  margin-top: 20px;
  align-items: center;
  word-break: break-all;
  // white-space: nowrap;
  // text-overflow: ellipsis;
  // overflow: hidden;
  // min-width: 0;
  // white-space: pre-wrap;
  // flex-wrap: wrap;
  //   border: 1px solid red;
}

.custom_card_details_extra_spacer {
  display: flex;
  //   justify-content: space-evenly;
  margin-left: 15px;
  margin-right: 15px;
  margin-top: 20px;
  align-items: center;
  word-break: break-all;
}

.custom_card_v-title-group {
  display: flex;
  flex-direction: column;
  //   border: 1px solid black;
  align-content: stretch;
  align-items: flex-end;
  line-height: 0;
}

.custom_card_v-title-start-group {
  display: flex;
  flex-direction: column;
  //   border: 1px solid black;
  //   align-content: stretch;
  align-items: flex-start;
  line-height: 0;
  //   margin: auto;
}
.custom_card_v-details-start-group {
  display: flex;
  flex-direction: column;
  //   border: 1px solid black;
  align-items: flex-start;
  line-height: 0;
  margin-right: 25%;
}
.invoicenumber {
  color: $lightblue;
  font-size: 24px;
  margin-top: 20px;
}

.rounded {
  border: 1px solid $yellow;
  border-radius: 25px;
  font-size: 12px;
  width: 50px;
  text-align: center;
  padding: 10px;
  color: $yellow;
}

.mb-40 {
  margin-bottom: 40px;
}
</style>