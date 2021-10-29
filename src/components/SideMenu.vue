<template>
  <aside>
    <div class="aside__item">
      <div class="aside-title">
        <strong>Сортировать</strong>
      </div>
      <div>
        <input
          @change="$emit('changeSort', sort)"
          v-model="sort"
          type="radio"
          name="sort"
          value="upPrice"
          checked
        />
        <label for="up-price">- по возрастанию цены</label>
      </div>

      <div>
        <input
          @change="$emit('changeSort', sort)"
          v-model="sort"
          type="radio"
          name="sort"
          value="downPrice"
        />
        <label for="down-price">- по убыванию цены</label>
      </div>

      <div>
        <input
          @change="$emit('changeSort', sort)"
          v-model="sort"
          type="radio"
          name="sort"
          value="travelTime"
        />
        <label for="time">- по времени в пути</label>
      </div>
    </div>
    <div class="aside__item">
      <div class="aside-title">
        <strong>Фильтровать</strong>
      </div>
      <div>
        <input
          @change="$emit('changeTransfer', transfer)"
          v-model="transfer"
          type="checkbox"
          name="filtr"
        />
        <label>- 1 пересадка</label>
      </div>

      <div>
        <input
          @change="$emit('changeWithoutTransfer', withoutTransfer)"
          v-model="withoutTransfer"
          type="checkbox"
          name="filtr"
        />
        <label>- без пересадок</label>
      </div>
    </div>
    <div class="aside__item">
      <div class="aside-title">
        <strong>Цена</strong>
      </div>
      <div>
        <div>
          <label for="price">От</label>
          <input
            @input="$emit('changeMin', minPrice)"
            v-model="minPrice"
            name="price"
            type="number"
          />
        </div>
        <div>
          <label for="price">До</label>
          <input
            @input="$emit('changeMax', maxPrice)"
            v-model="maxPrice"
            name="price"
            type="number"
          />
        </div>
      </div>
    </div>
    <div class="aside__item">
      <div class="aside-title">
        <strong>Авиокомпании</strong>
      </div>
      <div>
        <input
          @change="$emit('changeAirlanePolish', airlanePolish)"
          v-model="airlanePolish"
          type="checkbox"
        />
        <label>- LOT Polish Airlines</label>
      </div>

      <div>
        <input
          @change="$emit('changeAirlaneRus', airlaneRus)"
          v-model="airlaneRus"
          type="checkbox"
        />
        <label>- Аэрофлот - российские авиалинии</label>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  name: "SideMenu",

  data() {
    return {
      minPrice: 0,
      maxPrice: 100000,
      airlanePolish: false,
      airlaneRus: false,
      transfer: false,
      withoutTransfer: false,
      sort: "upPrice",
    };
  },
};
</script>

<style scoped>
aside {
  width: 20%;
  margin-left: 40px;
}
.aside__item {
  margin-top: 40px;
}
.aside-title {
  margin-bottom: 20px;
}
</style>