<template>
  <div class="home">
    <div
      class="w-full py-10 lg:py-5 border-b-8 "
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
        <div class="text-5xl font-black text-center text-white ">
          How is
          <input
            class="border-8 border-gray-200 text-gray-900 font-black mx-2 text-center  block md:inline"
            type="text"
            v-model="selectedCountry"
            size="10ch"
            list="allCountries"
          />
          doing ?
        </div>
        <div class="w-64 justify-end">
          <div class="w-48 h-48 p-4 mx-auto">
            <img
              class="w-full h-full object-contain mx-auto block h-auto p-3"
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
          <div
            class="status p-2 bg-red-800 text-red-200 text-center font-bold text-2xl"
            v-if="selectedCountryHealth === 'infected'"
          >
            AFFECTED
          </div>

          <div
            class="status p-2 bg-white text-green-500 text-center font-bold text-2xl"
            v-if="selectedCountryHealth === 'clear'"
          >
            NOT AFFECTED
          </div>

          <div
            class="status p-2 bg-white text-green-500 text-center font-bold text-xl"
            v-if="selectedCountryHealth === 'unknown'"
          >
            How to protect myself?
          </div>
        </div>
      </div>

      <datalist id="allCountries">
        <option v-for="country in allCountries" :key="country" :value="country">
        </option>
      </datalist>
    </div>
    <div class="md:flex px-8">
      <div class="md:w-1/2">
        <h1
          class="text-2xl text-gray-700 py-10 font-bold text-center md:text-right"
        >
          Affected countries
        </h1>

        <div
          class="affected-countries flex justify-center md:justify-end flex-wrap"
        >
          <!--      <img src="/images/virus.svg" alt="" />-->
          <div
            class="country"
            v-for="country in affectedCountries"
            :key="country"
            :class="country === selectedCountry ? 'bg-red-500' : 'bg-red-200'"
          >
            {{ country }}
          </div>
        </div>
      </div>
      <div class="w-10 hidden md:block">&nbsp;</div>
      <div class="md:w-1/2">
        <h1
          class="text-2xl text-gray-700 py-10 font-bold text-center md:text-left"
        >
          Unaffected countries
        </h1>

        <div
          class="unaffected-countries flex justify-center md:justify-start flex-wrap"
        >
          <div
            class="country "
            v-for="country in unaffectedCountries"
            :key="country"
            :class="
              country === selectedCountry ? 'bg-green-500' : 'bg-green-200'
            "
          >
            {{ country }}
          </div>
        </div>
      </div>
    </div>

    <div class="flex bg-gray-300 mt-20 py-10">
      <div class="container mx-auto flex items-center justify-center">
        <div class="text-xl font-bold uppercase text-gray-700 px-4">
          Share this page
        </div>

        <share-section />
      </div>
    </div>

    <div class="py-10 container mx-auto">
      <h2 class="text-2xl text-center">FAQ</h2>
      <ul class="faq grid grid-cols-3">
        <li>
          <label>What is the source ?</label>
          <p>
            The list of affected countries are from
            <a
              href="https://www.cdc.gov/coronavirus/2019-ncov/locations-confirmed-cases.html"
              >CDC.gov</a
            >
          </p>
        </li>
        <li>
          <label>When was this page last updated?</label>
          <p>Last updated: xx:xx:xx</p>
        </li>
        <li>
          <label>Is this updated automatically?</label>
          <p>
            No. I update the list whenever practically possible. Anyone can
            submit a PR to update the list
            <a href="https://github.com/MrSunshyne/covid19-affected-countries"
              >here</a
            >
          </p>
        </li>
      </ul>
    </div>

    <div class="flex hidden ">
      <pre>{{ affectedCountries }}</pre>

      <pre>{{ allCountries }}</pre>
    </div>
  </div>
</template>

<script>
import affectedCountries from "../data/affectedCountries";
import allCountries from "../data/allCountries";
import ShareSection from "../components/share-section";
export default {
  name: "home",
  data() {
    return {
      affectedCountries,
      allCountries,
      selectedCountry: "Mauritius"
    };
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
  methods: {},
  components: {
    ShareSection
  }
};
</script>

<style lang="scss">
.country {
  @apply text-sm p-2 m-2 rounded tracking-wide;
}

label {
  @apply font-bold my-4;
}

.faq li {
  margin-bottom: 2em;
}
</style>
