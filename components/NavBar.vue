<template>
  <div>
    <header class="bg-blue-500 w-full text-white shadow-lg navbar">
      <div class="container mx-auto flex justify-between p-5">
        <div class="">
          <nuxt-link :class="$device.isMobile ? 'flex row': 'flex'" to="/">
            <div class="mr-2">
              <img :style="$device.isMobile ? 'width: 5vw' : 'width:3vw;'" src="/logo.png">
            </div>
            <div>
              {{ config.public.HOTEL_NAME }}
            </div>
          </nuxt-link>
        </div>
        <nav class="hidden sm:flex space-x-4">
          <ul class="flex">
            <li class="sm:mr-5 pt-1">
              <nuxt-link class="hover:underline" to="/">
                Acasa
              </nuxt-link>
            </li>
            <li class="sm:mr-5">
              <el-dropdown>
                <button class="bg-blue-500 text-white py-2 px-4 rounded">
                  Camere
                  <el-icon class="el-icon--right">
                    <arrow-down />
                  </el-icon>
                </button>
                <template #dropdown>
                  <el-dropdown-menu>
                    <el-dropdown-item
                      v-for="room in roomsWithPrice"
                      :key="room.id"
                    >
                      <nuxt-link
                        :to="{ name: 'room-id', params: { id: room.id } }"
                      >
                        {{ room.name }}
                      </nuxt-link>
                    </el-dropdown-item>
                  </el-dropdown-menu>
                </template>
              </el-dropdown>
              <!-- <a href="#" class="hover:underline">Camere</a> -->
            </li>
            <li class="sm:mr-5 pt-1">
              <nuxt-link class="hover:underline" to="/Gallery">
                Galerie Foto
              </nuxt-link>
            </li>
            <li class="sm:mr-5 pt-1">
              <nuxt-link class="hover:underline" to="/contact">
                Contact
              </nuxt-link>
            </li>
            <li class="mx-2">
              <nuxt-link to="/Book">
                <button class="bg-blue-500 hover:bg-blue-700 text-white py-1 px-4 border border-blue-700 rounded">
                  Rezerva acum
                </button>
              </nuxt-link>
            </li>
          </ul>
        </nav>
        <div class="sm:hidden w-1/4 flex justify-center ">
          <button @click="isOpen = !isOpen">
            <span>☰</span>
          </button>
        </div>
      </div>
      <div
        v-if="isOpen"
        class="sm:hidden w-full flex justify-between meniuMobile"
      >
        <nav class="py-1 flex justify-center w-full">
          <ul class="text-center w-1/2">
            <li class="sm:mr-5 my-3 mt-5">
              <nuxt-link class="hover:underline" to="/">
                Acasa
              </nuxt-link>
            </li>
            <li class="sm:mr-5 my-3">
              <nuxt-link class="hover:underline" to="/Gallery">
                Galerie Foto
              </nuxt-link>
            </li>
            <li class="sm:mr-5 my-3">
              <el-dropdown>
                <button
                  class="border-transparent rooms"
                  color="bg-blue-500"
                >
                  <span class="text-lg"> Camere </span>
                </button>
                <template #dropdown>
                  <el-dropdown-menu>
                    <el-dropdown-item
                      v-for="room in roomsWithPrice"
                      :key="room.id"
                      style="margin-bottom:10px"
                    >
                      <nuxt-link exact :to="{ name: 'room-id', params: { id: room.id } }">
                        {{ room.name }}
                      </nuxt-link>
                    </el-dropdown-item>
                  </el-dropdown-menu>
                </template>
              </el-dropdown>
            </li>

            <li class="sm:mr-5 my-3">
              <nuxt-link class="hover:underline" to="/contact">
                Contact
              </nuxt-link>
            </li>
          </ul>
        </nav>
      </div>
    </header>
  </div>
</template>

<script setup>
import { ArrowDown } from '@element-plus/icons-vue'
const config = useRuntimeConfig()
const isOpen = ref(false)

const { data: rooms } = useFetch(
  `${config.public.API_URL}/rooms`
)
const roomsWithPrice = computed(() =>
  rooms.value ? rooms.value.filter(x => x.price) : []
)
const route = useRoute()

watch(
  route,
  (value) => {
    isOpen.value = false
  },
  { deep: true, immediate: true }
)
</script>

<style scoped>
.navbar {
  position: absolute;
  min-height: 10vh;
  z-index: 30;
}
.meniuMobile {
  z-index: 50;
}
.rooms {
  border: none;
}
.rooms:hover {
  background-color: rgb(59 130 246 / 1);
}
</style>
