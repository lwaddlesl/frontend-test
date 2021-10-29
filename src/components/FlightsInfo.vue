<template>
  <main>
    <div class="flight" v-for="(flight, index) in flights" :key="index">
      <div
        v-if="
          flight.flight.price.total.amount > minPrice &&
          flight.flight.price.total.amount < maxPrice
        "
      >
        <div
          v-if="
            (airlanePolish == true
              ? flight.flight.carrier.caption == 'LOT Polish Airlines'
              : false) ||
            (airlaneRus == true
              ? flight.flight.carrier.caption ==
                'Аэрофлот - российские авиалинии'
              : airlanePolish
              ? false
              : true)
          "
        >
          <div
            v-if="
              (transfer
                ? flight.flight.legs[0].segments.length > 1 ||
                  flight.flight.legs[1].segments.length > 1
                : false) ||
              (withoutTransfer
                ? flight.flight.legs[0].segments.length == 1 &&
                  flight.flight.legs[1].segments.length == 1
                : transfer
                ? false
                : true)
            "
          >
            <div class="blue-price">
              <div class="text-price">
                <p>{{ flight.flight.price.total.amount }} P</p>
                <p>Стоимость для одного взролого</p>
              </div>
            </div>
            <div v-for="(leg, index) in flight.flight.legs" :key="index">
              <span v-if="leg.segments[0].departureCity">
                {{ leg.segments[0].departureCity.caption }},
              </span>
              {{ leg.segments[0].departureAirport.caption }}
              <span class="blue">
                ({{ leg.segments[0].departureAirport.uid }})
              </span>
              ----------------------->
              <span v-if="leg.segments.length > 1">
                <span v-if="leg.segments[1].arrivalCity">
                  {{ leg.segments[1].arrivalCity.caption }},
                </span>
                {{ leg.segments[1].arrivalAirport.caption }}
                <span class="blue">
                  ({{ leg.segments[1].arrivalAirport.uid }})
                </span>
                <div class="time">
                  <div>
                    {{ leg.segments[0].departureDate.substr(11, 5) }}
                    <small class="blue"
                      >{{ leg.segments[0].departureDate.substr(5, 5) }}
                    </small>
                  </div>

                  {{ Math.floor(leg.duration / 60) }}ч
                  {{ leg.duration % 60 }}мин
                  <div>
                    <small class="blue"
                      >{{ leg.segments[1].arrivalDate.substr(5, 5) }}
                    </small>
                    {{ leg.segments[1].arrivalDate.substr(11, 5) }}
                  </div>
                </div>
                <p class="transfer">1 пересадка</p>
              </span>
              <span v-else>
                {{ leg.segments[0].arrivalCity.caption }},
                {{ leg.segments[0].arrivalAirport.caption }}
                <span class="blue">
                  ({{ leg.segments[0].arrivalAirport.uid }})
                </span>
                <div class="time">
                  <div>
                    {{ leg.segments[0].departureDate.substr(11, 5) }}
                    <small class="blue"
                      >{{ leg.segments[0].departureDate.substr(5, 5) }}
                    </small>
                  </div>

                  {{ Math.floor(leg.duration / 60) }}ч
                  {{ leg.duration % 60 }}мин
                  <div>
                    <small class="blue"
                      >{{ leg.segments[0].arrivalDate.substr(5, 5) }}
                    </small>
                    {{ leg.segments[0].arrivalDate.substr(11, 5) }}
                  </div>
                </div>
              </span>
              <p class="company">
                Рейс выплняет: {{ leg.segments[0].airline.caption }}
              </p>
              <hr v-if="index == 0" />
            </div>
            <button class="choose">Выбрать</button>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "FlightsInfo",
  props: {
    flights: Array,
    minPrice: Number,
    maxPrice: Number,
    airlanePolish: Boolean,
    airlaneRus: Boolean,
    transfer: Boolean,
    withoutTransfer: Boolean,
  },
};
</script>

<style scoped>
hr {
  border: none;
  background-color: rgb(0, 140, 255);
  height: 2px;
  margin-bottom: 10px;
}
main {
  margin: 10px;
  width: 80%;
}
.flight {
  height: auto;
  margin: 10px;
}
.blue {
  color: rgb(0, 140, 255);
}
.choose {
  width: 100%;
  height: 40px;
  background: rgb(204, 151, 53);
  color: white;
  text-transform: uppercase;
}
.blue-price {
  padding: 2px 0;
  margin: 10px 0;
  width: 100%;
  background-color: rgb(0, 38, 163);
  color: white;
  text-align: right;
}
.text-price {
  margin: 10px;
}
.time {
  margin: 10px;
  text-align: center;
  display: flex;
  justify-content: space-between;
}
.transfer {
  text-align: center;
  color: orange;
}
.company {
  margin-bottom: 10px;
}
</style>
