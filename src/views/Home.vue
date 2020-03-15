<template>
  <div class="home">
    <div
      class="w-full py-10 lg:py-5 border-b-8 border-t-8 "
      :class="
        selectedCountryHealth === 'unknown'
          ? 'bg-gray-500 border-gray-700'
          : selectedCountryHealth === 'infected'
          ? 'bg-red-500 border-red-700'
          : 'bg-green-500 border-green-700'
      "
    >
      <div
        class="container mx-auto flex flex-col lg:flex-row justify-center md:justify-around items-center"
      >
        <div class="">
          <div class="text-3xl sm:text-5xl font-black text-center text-white ">
            How is
            <input
              class="border-8 border-gray-200 text-gray-900 font-black mx-auto sm:mx-2 text-center  block md:inline"
              type="text"
              v-model="selectedCountry"
              size="8ch"
              list="allCountries"
            />
            doing ?
          </div>
          <p class="text-white py-2 text-center uppercase  text-sm">
            Type a country name to check status
          </p>
        </div>
        <div class="w-64 justify-end">
          <a
            class="status p-2 bg-red-800 text-red-200 text-center block font-bold text-2xl hover:bg-red-900"
            v-if="selectedCountryHealth === 'infected'"
            target="_blank"
            :href="
              `https://www.google.com/search?q=covid%2019%20in%20${selectedCountry}`
            "
          >
            AFFECTED
          </a>

          <a
            class="status p-2 bg-white text-green-500 text-center block font-bold text-2xl "
            v-if="selectedCountryHealth === 'clear'"
          >
            NOT AFFECTED
          </a>

          <a
            class="status p-2 bg-white text-green-500 text-center font-bold text-xl hover:bg-green-100"
            v-if="selectedCountryHealth === 'unknown'"
            href="https://www.cdc.gov/coronavirus/2019-ncov/protect/index.html"
            target="_blank"
          >
            How to protect myself?
          </a>
          <div class="w-48 h-48 p-4 mx-auto">
            <img
              class="w-full h-full object-contain mx-auto block h-auto p-3 virus-rotate"
              src="/images/virus.svg"
              alt=""
              v-if="selectedCountryHealth === 'infected'"
            />

            <img
              class="w-full h-full object-contain mx-auto block h-auto p-3"
              src="/images/clear.svg"
              alt=""
              v-if="selectedCountryHealth === 'clear'"
            />
            <img
              class="w-full h-full object-contain mx-auto block h-auto p-3"
              src="/images/nohandshake.svg"
              alt=""
              v-if="selectedCountryHealth === 'unknown'"
            />
          </div>
          <a
            class="status p-2 rounded-full block bg-white text-gray-700 text-center font-bold  text-sm hover:bg-gray-100"
            target="_blank"
            :href="
              `https://www.google.com/search?q=covid%2019%20in%20${selectedCountry}`
            "
          >
            Latest news on COVID-19 in {{ selectedCountry }}
          </a>
        </div>
      </div>

      <datalist id="allCountries">
        <option v-for="country in allCountries" :key="country" :value="country">
        </option>
      </datalist>
    </div>

    <div
      class="w-full last-updated text-center uppercase py-2 font-bold bg-gray-100 text-gray-500"
    >
      <div class="container mx-auto ">Last updated: {{ lastUpdated }}</div>
    </div>
    <div class="md:flex px-8 py-5">
      <div class="md:w-full">
        <!--        <h1 class="text-2xl text-gray-700 font-bold text-center md:text-right">-->
        <!--          Affected countries-->
        <!--        </h1>-->

        <div class="affected-countries flex justify-center flex-wrap">
          <!--          <div-->
          <!--            class="country hover:bg-red-400"-->
          <!--            v-for="country in affectedCountries"-->
          <!--            :key="country"-->
          <!--            :class="country === selectedCountry ? 'bg-red-500' : 'bg-red-200'"-->
          <!--            @click="setSelectedCountry(country)"-->
          <!--          >-->
          <!--            {{ country }}-->
          <!--          </div>-->

          <div
            class="country hover:bg-red-400"
            v-for="country in allCountries"
            :key="country"
            :class="
              affectedCountries.includes(country)
                ? 'bg-red-500'
                : 'bg-green-400'
            "
            @click="setSelectedCountry(country)"
          >
            {{ country }}
          </div>
        </div>
      </div>
      <!--      <div class="w-10 hidden md:block">&nbsp;</div>-->
      <!--      <div class="md:w-1/2">-->
      <!--        <h1 class="text-2xl text-gray-700 font-bold text-center md:text-left">-->
      <!--          Unaffected countries-->
      <!--        </h1>-->

      <!--        <div-->
      <!--          class="unaffected-countries flex justify-center md:justify-start flex-wrap"-->
      <!--        >-->
      <!--          <div-->
      <!--            class="country hover:bg-green-400"-->
      <!--            v-for="country in unaffectedCountries"-->
      <!--            :key="country"-->
      <!--            :class="-->
      <!--              country === selectedCountry ? 'bg-green-500' : 'bg-green-200'-->
      <!--            "-->
      <!--            @click="setSelectedCountry(country)"-->
      <!--          >-->
      <!--            {{ country }}-->
      <!--          </div>-->
      <!--        </div>-->
      <!--      </div>-->
    </div>

    <share-section />

    <faq-section :last-updated="lastUpdated" />

    <credit-section />
  </div>
</template>

<script>
import affectedCountries from "../data/affectedCountries";
import allCountries from "../data/allCountries";
import ShareSection from "../components/share-section";
import CreditSection from "../components/credits-section";
import FaqSection from "../components/faq-section";
export default {
  name: "home",
  data() {
    return {
      affectedCountries,
      allCountries,
      selectedCountry: "Mauritius",
      lastUpdated: "15th March 2020 @ 09:58 GMT"
    };
  },
  mounted() {
    this.selectedCountry = this.randomCountry();
  },
  computed: {
    unaffectedCountries() {
      return this.allCountries.filter(x => !this.affectedCountries.includes(x));
    },
    selectedCountryHealth() {
      if (this.allCountries.includes(this.selectedCountry)) {
        if (this.affectedCountries.includes(this.selectedCountry)) {
          return "infected";
        } else {
          return "clear";
        }
      }
      return "unknown";
    }
  },
  methods: {
    randomCountry() {
      return this.allCountries[
        Math.floor(Math.random() * this.allCountries.length)
      ];
    },
    setSelectedCountry(country) {
      this.selectedCountry = country;
    }
  },
  components: {
    ShareSection,
    CreditSection,
    FaqSection
  }
};
</script>

<style lang="scss">
.country {
  @apply text-xs p-2 m-2 rounded tracking-wide cursor-pointer;
}

label {
  @apply font-bold my-4;
}

.virus-rotate {
  animation: rotate 5s infinite linear;
}

@keyframes rotate {
  to {
    transform: rotate(360deg);
  }
}

.faq a,
.built-using a {
  @apply underline;
}

.built-using li {
  margin: 10px;
}
.faq li {
  margin-bottom: 2em;
}
</style>
