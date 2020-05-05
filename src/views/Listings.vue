<template>
  <div class="content">
    <transition enter-active-class="animated fadeInRight">
      <div v-show="showtitle" class="header">
        <img class="arrow" src="@/assets/images/button-el.png" />
        <div class="animatetext">
          <p class="mtext-light">
            Show me
            <span class="mtext-bold">invoices</span> of
            <span class="mtext-bold">STF Belgium</span>
            from
            <span class="mtext-bold">January</span> to
            <span class="mtext-bold">April</span> of
            <span class="mtext-bold">2018</span>
          </p>
        </div>
      </div>
    </transition>

    <div class="stackcards">
      <div v-for="(card,index) in cards" :key="card.id">
        <transition leave-active-class="animated fadeIn">
          <div @click="loaddetails">
            <Vue2InteractDraggable
              @draggedUp="draggedUp"
              @draggedDown="draggedDown"
              :interact-y-threshold="5"
              :interact-lock-swipe-down="interactLockSwipeDown"
              :interact-lock-swipe-left="interactLockSwipeLeft"
              :interact-lock-swipe-right="interactLockSwipeRight"
            >
              <ParentCard
                :class="{  stackcards_child: index == 0, stackcards_child_bg:index ==1  , stackcards_child_normal: index >1 }"
                :invoicenumber="card.invoicenumber"
                :price="card.price"
                :buyername="card.buyername"
                :sellername="card.sellername"
                :date="card.date"
                :address="card.address"
                :showdetailsperent="showdetails"
              />
            </Vue2InteractDraggable>
          </div>
        </transition>
      </div>
    </div>

    <div class="walletholder">
      <transition enter-active-class="animated fadeIn" leave-class="animated fadeIn">
        <img class="walletlogo" v-show="showdetails" src="@/assets/images/icon-wallet.png" />
      </transition>
    </div>
  </div>
</template>

<script>
import ParentCard from "../components/ParentCard";
import { Vue2InteractDraggable } from "vue2-interact";

export default {
  name: "Listings",
  data() {
    return {
      showtitle: false,
      interactLockSwipeDown: false,
      interactLockSwipeLeft: true,
      interactLockSwipeRight: true,
      showdetails: false,
      cardwidth: 500,
      cards: [
        {
          id: 0,
          invoicenumber: "H3110017",
          price: "€ 204",
          buyername: "STF France",
          sellername: "STF Belgium",
          date: "14 Feb 2018",
          address: "0x4E5748...c81868F6"
        },
        {
          id: 1,
          invoicenumber: "H3110018",
          price: "€ 204",
          buyername: "STF France",
          sellername: "STF England",
          date: "14 July 2019",
          address: "0x4E5748...c81868F7"
        },
        {
          id: 2,
          invoicenumber: "H3110019",
          price: "€ 204",
          buyername: "STF France",
          sellername: "STF Germany",
          date: "14 March 2020",
          address: "0x4E5748...c81868F8"
        }
      ]
    };
  },
  mounted() {
    var vm = this;
    vm.showtitle = true;
  },
  watch: {
    cards: function(val) {
      console.log(this.cards + ", " + val);
    }
  },
  methods: {
    draggedUp() {
      console.log("dragged up!");
      this.cards.shift();
      // this.hideCard();
    },
    draggedDown() {
      console.log("dragged down!");
      this.cards.shift();
      // this.hideCard();
    },
    loaddetails() {
      console.log("load details");
      this.showdetails = !this.showdetails;

      if (this.showdetails) {
        this.cardwidth = 700;

        this.cards = [
          {
            id: 0,
            invoicenumber: "H3110017",
            price: "€ 204",
            buyername: "STF France",
            sellername: "STF Belgium",
            date: "14 Feb 2018",
            address: "0x4E5748...c81868F6"
          }
        ];
      } else {
        this.cardwidth = 500;
        this.cards = [
          {
            id: 0,
            invoicenumber: "H3110017",
            price: "€ 204",
            buyername: "STF France",
            sellername: "STF Belgium",
            date: "14 Feb 2018",
            address: "0x4E5748...c81868F6"
          },
          {
            id: 1,
            invoicenumber: "H3110018",
            price: "€ 204",
            buyername: "STF France",
            sellername: "STF England",
            date: "14 July 2019",
            address: "0x4E5748...c81868F7"
          },
          {
            id: 2,
            invoicenumber: "H3110019",
            price: "€ 204",
            buyername: "STF France",
            sellername: "STF Germany",
            date: "14 March 2020",
            address: "0x4E5748...c81868F8"
          }
        ];
      }
      // this.callChildFunction();
    }
  },

  components: {
    // HelloWorld
    ParentCard,
    Vue2InteractDraggable
  }
};
</script>

<style lang="scss" scoped>
@import "../utils/color.scss";
@import "../utils/dimensions.scss";

.stackcards {
  position: relative;
  //   background-color: $greytext;
  //border: 1px solid black;

  height: 80vh;
  margin: 0 auto;
}

.stackcards_child {
  position: absolute;
  left: 0;

  right: 0;
  //   border: 1px solid black;
  width: 100%;
  z-index: 2;
  margin: 0 auto;
}

.stackcards_child_bg {
  position: absolute;
  left: 0;
  right: 0;
  margin: 20px auto;
  //   border: 1px solid red;
  width: 95%;
  z-index: 1;
  opacity: 50%;

  -webkit-filter: blur(1px);
  -moz-filter: blur(1px);
  -o-filter: blur(1px);
  -ms-filter: blur(1px);
  filter: blur(1px);
}

.stackcards_child_normal {
  position: absolute;
  left: 0;
  //   right: 0;
  //   top: 10;
  right: 0;
  //   margin-top: 50px;
  margin: 40px auto;
  //   border: 1px solid red;
  width: 90%;
  z-index: 0;
  opacity: 30%;

  -webkit-filter: blur(2px);
  -moz-filter: blur(2px);
  -o-filter: blur(2px);
  -ms-filter: blur(2px);
  filter: blur(2px);
}

p {
  font-weight: 200;
}

.walletholder {
  width: 100%;
  // border: 1px solid red;
  text-align: end;
}

.walletlogo {
  // border: 1px solid red;
  // width: 100%;
  // position: absolute;
  // bottom: 25px;
  // right: 25px;
  background-color: $lightblue;
  border-radius: 50px;
  padding: 5px;
  color: white;
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

.arrow {
  height: 35px;
  margin-right: 5px;
}
.mtext-bold {
  font-size: 18px;
  color: $lightboldfont;
}

.mtext-light {
  font-size: 18px;
  color: $lightfont;
}

.custom-card {
  background-color: $white;
  width: 50%;
  //   height: 400px;
  padding: 20px;
  border-radius: 10px;
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

.custom_card_details_spacer {
  display: flex;
  //   justify-content: space-evenly;
  margin-left: 20px;
  margin-right: 20px;
  margin-top: 20px;
  align-items: center;
  //   border: 1px solid red;
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