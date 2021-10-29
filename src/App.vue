<template>
  <div id="app">
    <SideMenu
      @changeMin="minPrice = Number($event)"
      @changeMax="maxPrice = Number($event)"
      @changeAirlanePolish="airlanePolish = $event"
      @changeAirlaneRus="airlaneRus = $event"
      @changeTransfer="transfer = $event"
      @changeWithoutTransfer="withoutTransfer = $event"
      @changeSort="sort = $event"
    />
    <Flights-info
      :minPrice="minPrice"
      :maxPrice="maxPrice"
      :flights="f"
      :airlanePolish="airlanePolish"
      :airlaneRus="airlaneRus"
      :transfer="transfer"
      :withoutTransfer="withoutTransfer"
    />
  </div>
</template>

<script>
import FlightsInfo from "./components/FlightsInfo.vue";
import SideMenu from "./components/SideMenu.vue";
import data from "./assets/flights";

export default {
  name: "App",
  components: {
    SideMenu,
    FlightsInfo,
  },
  watch: {
    sort: function () {
      if (this.sort == "upPrice") {
        this.f = this.flights;
      } else if (this.sort == "downPrice") {
        this.f = this.reverseFlights;
      } else if (this.sort == "travelTime") {
        this.f = this.travelFlights;
      }
    },
  },
  data() {
    return {
      data,
      f: null,
      flights: null,
      reverseFlights: null,
      travelFlights: null,
      minPrice: 0,
      maxPrice: 100000,
      airlanePolish: false,
      airlaneRus: false,
      transfer: false,
      withoutTransfer: false,
      sort: "upPrice",
    };
  },
  mounted() {
    this.flights = data.result.flights;
    this.flights.sort((a, b) => {
      return a.flight.price.total.amount - b.flight.price.total.amount;
    });
    this.reverseFlights = JSON.parse(JSON.stringify(this.flights));
    this.reverseFlights.reverse();
    this.travelFlights = JSON.parse(JSON.stringify(this.flights));
    this.travelFlights.sort((a, b) => {
      return (
        a.flight.legs[0].duration +
        a.flight.legs[1].duration -
        (b.flight.legs[0].duration + b.flight.legs[1].duration)
      );
    });
    this.f = JSON.parse(JSON.stringify(this.flights));
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
#app {
  display: flex;
}
</style>
