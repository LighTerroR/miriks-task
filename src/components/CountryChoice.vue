/* eslint-disable vuejs-accessibility/click-events-have-key-events */
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
        class="country-select__country-wrapper"
        @click="changeCountry('ru')"
      >
        <img
          src="@/assets/img/ru.png"
          alt="Russia"
          title="Russia"
          class="country-select__country"
        >
      </div>
      <div
        class="country-select__country-wrapper"
        @click="changeCountry('uk')"
      >
        <img
          src="@/assets/img/uk.png"
          alt="Great Britain"
          title="Great Britain"
          class="country-select__country"
        >
      </div>
      <div
        class="country-select__country-wrapper"
        @click="changeCountry('usa')"
      >
        <img
          src="@/assets/img/usa.png"
          alt=""
          title="United States of America"
          class="country-select__country"
        >
      </div>
      <div
        class="country-select__country-wrapper"
        @click="changeCountry('ua')"
      >
        <img
          src="@/assets/img/ua.png"
          alt="Ukraine"
          title="Ukraine"
          class="country-select__country"
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CountryChoice',
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
