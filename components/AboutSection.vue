<template>
  <div>
    <div style="margin-top: 5vh">
      <div ref="target1" class="text-2xl text-center">
        Despre {{ config.public.HOTEL_NAME }}
      </div>
      <div class="flex justify-center mt-5">
        <div class="details">
          {{ config.public.aboutDetails }}
        </div>
      </div>
      <div v-if="!$device.isMobile" class="flex justify-center mt-5">
        <div class="flex row" style="width: 80vw">
          <div
            v-for="(item, index) in filteredList"
            :key="index"
            :data-index="index"
            style="height: auto; background: red"
            class="mx-2 mb-2 flex-1"
          >
            <RoomCard
              :link="item.link"
              :hide-overlay="item.hideOverlay"
              :image="item.image"
              :room-name="item.name"
              :details="item.details"
              buttonText="Vezi"
              :title="item.title"
            />
          </div>
        </div>
      </div>
      <div v-else class="pa-2">
        <Customfade>
          <div
            v-for="(item, index) in filteredList"
            :key="index"
            :data-index="index"
            style="height: auto; background: red"
            class="mx-2 mb-2"
          >
            <RoomCard
              :link="item.link"
              :hide-overlay="item.hideOverlay"
              :image="item.image"
              :room-name="item.name"
              :details="item.details"
              :title="item.title"
            />
          </div>
        </Customfade>
      </div>
    </div>
  </div>
</template>

<script setup>

const config = useRuntimeConfig()
// TODO -Customize or fetch from api
const list = ref([
  {
    title: 'Apartament',
    link: '17',
    image: 'https://teleptean.s3.eu-west-3.amazonaws.com/DSC_00781_ff602c0994.jpg',
    hideOverlay: false,
    details:
      'Cameră frumoasă și spațioasă, cu paturi king-size și un confort sporit. Începeți dimineața într-un cadru elegant cu micul dejun gratuit, bogat si variat.'
  },
  {
    title: 'Camera dubla',
    link: '15',
    image: 'https://teleptean.s3.eu-west-3.amazonaws.com/DSC_00967_bff4aadeee.jpg',
    hideOverlay: true,
    details: 'Cameră frumoasă și spațioasă, cu paturi king-size și un confort sporit'
  }
])
const { filteredList, target: target1 } = useCustomFade(list)
</script>

<style scoped>
@media only screen and (min-width: 600px) {
  .details {
    width: 60vw;
  }
}

@media only screen and (max-width: 600px) {
  .details {
    width: 100vw;
    font-size: 8px;
    padding: 10px;
  }
}
</style>
