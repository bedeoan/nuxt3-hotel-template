<template>
  <div>
    <div v-for="room in roomsWithPrice" :key="room.id" class="flex row">
      <div class="flex-1 flex row">
        <div v-if="room.profile_image">
          <div v-if="room && room.images" class="flex justify-center mb-5">
            <ImageGallery
              :one-image-url="room.profile_image.url"
              :images="room.images"
              :index="index"
              :disable-scroll="true"
              @close="index = null"
            />
          </div>
        </div>
        <div v-else class="flex-1">
          -
        </div>
      </div>
      <div class="pt-2 flex-1">
        <div class="text-center mb-5">
          {{ room.name }}
        </div>
        <div
          v-for="option in room.options"
          :key="option.id"
          style="margin-left: 5vw"
        >
          <el-icon><Check /></el-icon>
          {{ option.name }}
        </div>
        <div style="margin-left: 5vw" class="mt-2">
          <nuxt-link :to="{ name: 'room-id', params: { id: room.id } }">
            <button>
              <el-icon><InfoFilled /></el-icon>
              {{ config.public.moreInfo }}
            </button>
          </nuxt-link>
        </div>
      </div>

      <div class="flex-1 pt-2 items-center text-center">
        <el-icon v-for="pers in room.pers" :key="pers">
          <User />
        </el-icon>
        <div class="text-neutral-300">
          x {{ room.pers }} pers
        </div>
      </div>
      <div class="flex-1 pt-2 text-center">
        {{ room.price }}
        {{ config.public.currency }} / {{ config.public.camera }}
      </div>
      <div class="pt-2">
        <BookButton :label="config.public.bookNow" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { User, Check, InfoFilled } from '@element-plus/icons-vue'
const config = useRuntimeConfig()
const props = defineProps({
  roomsWithPrice: Array
})
</script>
