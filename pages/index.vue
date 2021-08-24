<template>
  <!-- <template @keypress.space="On_KeyPress"> -->
  <!-- <div class="container" tabindex="-1" @keyup.space="On_KeyPress"> -->
  <div class="h-screen w-screen overflow-hidden">
    <div
      class="bg-black h-screen flex flex-wrap content-center bg-img overflow-hidden"
    ></div>
    <div class="w-screen h-screen">
      <div
        class="w-full mt-20 p-3 top-0 left-0 border-l-2 absolute md:mt-56 md:ml-32 md:w-3/4 sm:ml-12"
      >
        <div
          :class="quote ? '' : 'animate-pulse bg-purple-300 h-16 rounded m-4'"
          class="w-full"
        >
          <h2 v-if="quote" class="m-4 text-white text-3xl">
            {{ quote }}
          </h2>
        </div>
        <div
          :class="
            author
              ? 'w-auto'
              : 'animate-pulse bg-purple-300 h-12 rounded w-1/3 m-4'
          "
        >
          <p v-if="author" class="m-4 text-white uppercase">- {{ author }}</p>
        </div>
        <div
          :class="
            quote
              ? ''
              : 'animate-pulse bg-purple-300 h-16 rounded m-4 w-48 h-12'
          "
          class=""
        >
          <button
            v-if="quote"
            class="border-2 border-solid border-white p-2 rounded m-4 mb-0 text-white"
            @click="getQuote()"
          >
            Generate New
          </button>
        </div>
        <a href="#" class="" target="_blank" rel="noopener noreferrer"></a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      quote: '',
      author: '',
    }
  },
  async created() {
    await this.getQuote()
  },
  methods: {
    async getQuote() {
      const config = { headers: { Accept: 'application/json' } }
      try {
        const res = await axios.get(
          'https://api.quotable.io/random?tags=inspirational|success|life|business',
          config
        )
        this.quote = res.data.content
        this.author = res.data.author
        // eslint-disable-next-line no-console
        console.log('Quote', res.data.content)
        console.log('Tag', res.data.tags)
      } catch (error) {
        // eslint-disable-next-line no-console
        console.log('Error Message', error)
      }
    },
  },
}
</script>

<style>
/* eslint-disable-next-line no-console */
.bg-img {
  width: 5000px;
  background: url(~/assets/1.jpg) repeat-x;
  background-position: center center;
  background-size: contain;
  background-blend-mode: overlay;
  background-color: #000000e0;
  animation: slide 200s linear infinite;
}
@keyframes slide {
  0% {
    transform: translate3d(0, 0, 0);
  }
  100% {
    transform: translate3d(-1692px, 0, 0);
  }
}
ul {
  list-style: none;
}
svg {
  width: 25px;
  fill: #fff;
}
</style>
