<template>
  <div class="country-select">
    <div
      class="country-select__active"
      @click="submenu = !submenu"
    >
      <img
        :src="require(`@/assets/img/${country}.png`)"
        class="country-select__country"
        alt=""
      >
      <span class="country-select__arrow" />
    </div>
    <div
      class="country-select__countries"
      :class="{'_active': submenu}"
    >
      <div
        v-for="massCountry, index in countries"
        :key="index"
        class="country-select__country-wrapper"
        @click="changeCountry(massCountry)"
      >
        <img
          :src="require(`@/assets/img/${massCountry}.png`)"
          :alt="massCountry"
          :title="massCountry"
          class="country-select__country"
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CountryChoice',
  props: {
    countries: {
      type: Array,
      default: () => [],
    },
  },
  emits: ['get-сountry'],
  data() {
    return {
      country: 'ru',
      submenu: false,
    };
  },
  methods: {
    changeCountry(country) {
      this.country = country;
      this.submenu = !this.submenu;
      this.$emit('get-сountry', country);
    },
  },
};
</script>

<style lang="scss" scoped>
.country-select {
  position: relative;
  width: 100px;
  height: 45px;
  margin-right: 10px;

  &__active {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 100%;
    height: 100%;
    border: 1px solid #000;
    border-radius: 4px;
    cursor: pointer;
  }

  &__country {
    width: 40px;
    height: 40px;
  }

  &__country-wrapper {
    display: flex;
    justify-content: center ;
    width: 100%;
    cursor: pointer;

    &:hover {
      background-color: rgb(4, 8, 255);
    }
  }

  &__arrow {
    width: 0;
    height: 0;
    border-top: 10px solid #000;
    border-right: 5px solid transparent;
    border-left: 5px solid transparent;
  }

  &__countries {
    position: absolute;
    top: 110%;
    display: none;
    width: 100%;
    border: 1px solid #000;
    border-radius: 4px;
  }
}

._active {
  display: block;
}
</style>
