<template>
  <div style="height: 45vh; position: relative" class="flex items-center">
    <div>
      <img class="coverimg" :src="config.public.behappyCoverImg">
      <div class="overlay" />
      <div class="overlaytext">
        <div class="text-2xl">
          {{ config.public.behappy }}
        </div>
        <div class="my-5 px-2">
          {{ config.public.behappyDetails }}
        </div>
        <div class="mb-2">
          {{ config.public.behappyDetails2 }}
        </div>
        <nuxt-link to="/contact">
          <button
            class="bg-blue-500 hover:bg-blue-700 text-sm text-white py-2 px-4 border border-blue-700 rounded"
          >
            {{ config.public.behappyContact }}
          </button>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script setup>
const config = useRuntimeConfig()
</script>
<style scoped>
.coverimg {
  width: 100vw;
  height: 45vh;
  object-fit: cover;
}
.overlay {
  position: absolute; /* Sit on top of the page content */
  display: none; /* Hidden by default */
  width: 100%; /* Full width (cover the whole page) */
  height: 45vh; /* Full height (cover the whole page) */
  top: 0;
  left: 0;
  right: 0;
  display: block;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.861); /* Black background with opacity */
  z-index: 2; /* Specify a stack order in case you're using a different order for other elements */
  cursor: pointer; /* Add a pointer on hover */
}
.overlaytext {
  position: absolute; /* Sit on top of the page content */
  display: none; /* Hidden by default */
  width: 100%; /* Full width (cover the whole page) */
  height: 32vh; /* Full height (cover the whole page) */
  top: 50%;
  transform: translate(-50%, -50%); /* This is important to truly center the child */
  left: 50%;
  display: block;
  bottom: 0;
  z-index: 5; /* Specify a stack order in case you're using a different order for other elements */
  cursor: pointer;
  text-align: center;
  color: #ffffff;
  font-family: "Poppins", Sans-serif;
}
</style>
