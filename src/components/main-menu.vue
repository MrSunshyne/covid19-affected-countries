<template>
  <div class="bg-gray-800 text-white">
    <div
      class="main-menu container mx-auto font-bold lg:flex justify-center md:justify-between items-center px-8 md:px-0 py-3 md:py-10"
    >
      <router-link class="hidden text-center md:inline text-3xl" :to="'/'"
        >COVID-19 Status</router-link
      >

      <p>
        A simple tool to check if a country has been affected by COVID-19 until
        now
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.main-menu {
  /* @apply bg-black; */

  ul {
    list-style: none;
    display: flex;
    justify-content: center;

    li {
      position: relative;
      button {
        margin: 10px;
      }

      a {
        padding: 10px;
        display: block;
        @apply border-2;
        text-decoration: none;
        border-color: transparent;
        cursor: pointer;
      }
    }
  }
}

@screen sm {
  .main-menu {
    ul {
      li {
        padding: 10px;

        button {
          margin: 10px;
        }
        a {
          padding: 10px;
        }
      }
    }
  }
}
</style>
