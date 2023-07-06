<template>
  <div>
    <div class="flex justify-center bg-green-400 h-16">
      <span class="text-xl text-white py-4">QR Generator</span>
    </div>
    <div class="flex justify-between mx-40">
      <div class="w-1/2 my-10">
        <InputForm @btn-generate="onGenerate" @is-generated="isDisplay"/>
        <div v-if="isGenerated">
          <QrDisplay :qr="qrCode" @btn-download="saveQR"/>
        </div>
      </div>
      <div class="w-1/2 mx-20 my-10">
        <img src="../assets/img.jpg" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import QRCode from 'qrcode'
import InputForm from '@/components/InputForm.vue'
import QrDisplay from '@/components/QrDisplay.vue'

export default {
  name: 'HomeView',
  components: {
    InputForm,
    QrDisplay,
  },
  data() {
    return {
      qrCode: '',
      isGenerated: false,
      imgFile: null
    }
  },
  methods: {
    async onGenerate(url) {
      await QRCode.toDataURL(url, { errorCorrectionLevel: 'H', version: 6 })
      .then(response => {
        this.qrCode = response
      })
      .catch(error => {
        console.error(error)
      })
    },
    isDisplay() {
      this.isGenerated = true
    },
    async saveQR(qrSource, title) {
      title = 'qr_code.png'

      const response = await fetch(qrSource)
      const blobImage = await response.blob()
      const url = URL.createObjectURL(blobImage)
      Object.assign(document.createElement('a'), { href: url, download: title}).click()
      URL.revokeObjectURL(url)
    }
  },
}
</script>
