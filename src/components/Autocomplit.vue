<template>
  <div class="autocomplit">
    <country-choice
      :countries="countries"
      @get-сountry="getCountry"
    />
    <company-choice
      :companies="companies[currentCountry]"
      :filter="filter"
    />
  </div>
</template>

<script>
import CountryChoice from '@/components/CountryChoice.vue';
import CompanyChoice from '@/components/CompanyChoice.vue';

export default {
  name: 'CustomAutocomplit',
  components: {
    CountryChoice,
    CompanyChoice,
  },
  props: {
    countries: {
      type: Array,
      default: () => ['ru', 'uk', 'usa', 'ua'],
    },
    companies: {
      type: Object,
      default: () => this.$store.state.company,
    },
    filter: {
      type: Function,
      default(companies) {
        return companies.filter((company) => {
          // eslint-disable-next-line no-restricted-syntax
          for (const info of Object.values(company)) {
            if (info.toLowerCase().match(this.search.toLowerCase())) {
              return true;
            }
          }
          return false;
        });
      },
    },
  },
  data() {
    return {
      currentCountry: 'ru',
    };
  },
  methods: {
    getCountry(country) {
      this.currentCountry = country;
    },
  },
};
</script>

<style lang="scss" scoped>
.autocomplit {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}
</style>
