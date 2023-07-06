<template>
  <div class="flex justify-center ">
    <div class="">
      <img :src="qr" width="230" class="ring-1 ring-green-400"/>
      <div class="text-center bg-red-500 my-4 py-2 rounded cursor-pointer hover:bg-red-600">
        <button @click="$emit('btn-download',qr)" class="text-white">Download</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'QR Display',
  props: {
    qr: String,
  },
}

</script>