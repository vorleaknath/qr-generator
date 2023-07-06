<template>
  <div class="mx-10">
    <form @submit="onSubmit" class="py-5 px-6">
      <div class="mb-4 text-sm">
          <h3 class="font-bold text-xl mb-3">QR Code Generator</h3>
          <p class="mb-2">QR Codes allow smartphone users to access your website simply and quickly.</p>
          <p>Enter your URL below to generate a QR Code and download the image.</p>
        </div>
      <div>
        <input type="url" placeholder="Enter url" class="w-full bg-inherit border border-green-400 rounded py-2 px-3 text-gray-500 focus:outline-none" v-model="url">
      </div>
      <div v-if="isError">
        <p class="text-red-400 text-xs py-2">Please enter url for generating</p>
      </div>
      <div class="bg-green-400 rounded my-6 text-center hover:bg-green-600">
        <input type="submit" value="Generate" class="text-white py-2 cursor-pointer">
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Input Form',
  data() {
    return {
      url: '',
      isError: false,
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()

      if(this.url != ''){
        this.$emit('btn-generate', this.url, this.size)

        this.$emit('is-generated')
        this.url=''
      }else {
        this.isError = true
      }
    },
  }

}

</script>