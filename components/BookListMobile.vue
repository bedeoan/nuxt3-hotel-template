<template>
  <div>
    <div v-for="room in roomsWithPrice" :key="room.id" class="mb-5">
      <div>
        <div v-if="room.profile_image">
          <div v-if="room && room.images" class="flex justify-center mb-5">
            <ImageGallery
              :one-image-url="room.profile_image.url"
              :images="room.images"
              :index="0"
              :disable-scroll="true"
              @close="index = null"
            />
          </div>
        </div>
        <div v-else class="">
          -
        </div>
      </div>
      <div class="pt-2">
        <div class="ml-5 text-2xl mb-5">
          {{ room.name }}
          <div />
        </div>
        <div v-for="option in room.options" :key="option.id" class="ml-5">
          <el-icon><Check /></el-icon>
          {{ option.name }}
        </div>
      </div>

      <div class="pt-2 flex ml-5">
        <div class="mr-2">
          <el-icon v-for="pers in room.pers" :key="pers">
            <User />
          </el-icon>
        </div>
        <div class="text-neutral-300">
          x {{ room.pers }} pers
        </div>
        <nuxt-link
          class="ml-5"
          :to="{ name: 'room-id', params: { id: room.id } }"
        >
          <button
          >
            <el-icon>
              <InfoFilled />
            </el-icon>
            {{ config.public.moreInfoMobile }}
          </button>
        </nuxt-link>
      </div>
      <div class="pt-2 ml-5 flex row">
        <div>
          {{ room.price }}
          {{ config.public.currency }} / {{ config.public.camera }}
        </div>
      </div>
      <div class="pt-2 ml-5">
        <BookButton label="Rezerva Acum" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { User, Phone, Check, InfoFilled } from '@element-plus/icons-vue'
const config = useRuntimeConfig()
const props = defineProps({
  roomsWithPrice: Array
})
</script>
