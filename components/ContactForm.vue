<template>
  <div :class="$device.isMobile ? '' : 'flex'" style="margin-top: 50px; margin-bottom: 50px">
    <div class="flex-1 flex justify-center mt-5">
      <div :style="$device.isMobile ? 'width: 96%;margin-left:2vw': 'width:300px'">
        <div>
          <div class="text-2xl mb-5">
            Contacteaza-ne
          </div>
        </div>
        <div>
          <div class="text-2xl mb-5">
            <el-icon size="large">
              <Location />
            </el-icon>
            Address
          </div>

          <div class="ml-3">
            {{ address }}
          </div>

          <div class="text-2xl mt-5">
            <el-icon size="large">
              <Phone />
            </el-icon>
            Phone Number
          </div>
          <div class="ml-2">
            <div class="my-2">
              <button
                class="text-blue-500 py-2 px-4"
                @click="callClient(config.public.CONTACT_PHONE1)"
              >
                {{ config.public.CONTACT_PHONE1 }}
              </button>
            </div>
            <!-- <div>
              <el-button
                link
                @click="callClient(config.public.CONTACT_PHONE2)"
                >{{ config.public.CONTACT_PHONE2 }}</el-button
              >
            </div> -->
          </div>

          <div class="text-2xl mt-5">
            <el-icon size="large">
              <Message />
            </el-icon>
            Email Address
          </div>
          <div class="ml-3">
            {{ config.public.CONTACT_EMAIL }}
          </div>
          <!-- <div>
            <el-button
              size="large"
              class="mt-5"
              type="primary"
              @click="callClient(config.public.CONTACT_PHONE2)"
            >
              <el-icon class="mr-2" size="large"><Phone /></el-icon>
              Contact
            </button>
          </div> -->
        </div>
      </div>
    </div>
    <div class="flex-1 mt-5 p-1">
      <client-only>
        <GoogleMap
          :api-key="config.public.GOOGLE_API"
          :style="$device.isMobile ? 'width: 100vw; height:100vw' : 'width:100%;height:60vh' "
          :center="center"
          :zoom="10"
        >
          <Marker :options="{ position: center }" />
        </GoogleMap>
      </client-only>
    </div>
  </div>
</template>

<script setup>
import { defineComponent } from 'vue'
import { GoogleMap, Marker } from 'vue3-google-map'
import { Location, Phone, Message } from '@element-plus/icons-vue'
const config = useRuntimeConfig()
const center = {
  lat: parseFloat(config.public.LATITUDE),
  lng: parseFloat(config.public.LONGITUDE)
}
const address = 'Str. Unirii 1C, Ocna Sugatag,Maramures, România,'
const callClient = (phone) => {
  const nodash = phone.replace(/-/g, '')
  window.location = 'tel:+4' + nodash
}
</script>
