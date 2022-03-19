<template>
  <div class="company-input">
    <input
      v-model="search"
      class="company-input__input"
      type="text"
      placeholder="Type company info"
      @focus="open = true"
    >
    <div
      class="company-input__companies"
      :class="{'_active': open}"
    >
      <template v-if="filteredCompanies.length === 0">
        <p class="company-input__not-found">
          Company was not found
        </p>
      </template>
      <template v-else>
        <div
          v-for="company, index in filteredCompanies"
          :key="index"
          class="company-input__company"
          @click="setSearch(company.name)"
        >
          <p class="company-input__name">
            {{ company.name }}
          </p>
          <span
            class="company-input__phone"
            :title="`+${company.contactPhone}`"
          >+{{ company.contactPhone }}</span>
          <span
            class="company-input__inn"
            :title="company.inn"
          >{{ company.inn }}</span>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CompanyChoice',
  props: {
    companies: {
      type: Array,
      default: () => [],
    },
    filter: {
      type: Function,
      default() {},
    },
  },
  data() {
    return {
      search: '',
      open: false,
    };
  },
  computed: {
    filteredCompanies() {
      return this.filter(this.companies);
    },
  },
  methods: {
    setSearch(companyName) {
      this.search = companyName;
      this.open = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.company-input {
  position: relative;
  width: 300px;
  height: 45px;
  font-family: sans-serif;
  font-style: normal;
  font-weight: normal;

  &__input {
    width: 100%;
    height: 100%;
    padding: 5px 10px;
    border: 1px solid #000;
    border-radius: 4px;
    font-size: 20px;

    &::placeholder {
      font-size: 20px;
    }
  }

  &__companies {
    position: absolute;
    top: 110%;
    display: none;
    flex-direction: column;
    align-items: center;
    width: 100%;
    border: 1px solid #000;
    border-radius: 4px;
  }

  &__not-found {
    padding: 5px 10px;
    font-style: italic;
    font-size: 18px;
    line-height: 120%;
    color: rgba(0, 0, 0, 0.7);
  }

  &__company {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    width: 100%;
    padding: 5px 10px;
    color: #000;
    cursor: pointer;

    &:hover {
      background-color: rgb(4, 8, 255);
      color: #FFF;
    }
  }

  &__name {
    width: 100%;
    font-weight: bold;
    font-size: 18px;
    line-height: 120%;
    text-align: center;
  }

  &__phone,
  &__inn {
    overflow: hidden;
    max-width: 48%;
    font-size: 16px;
    line-height: 150%;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
}

._active {
  display: flex;
}
</style>
