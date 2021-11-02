<template>
  <div >
    <cld-image ref="ref"  :public-id="publicId" width="1000">
      <cld-transformation crop="fit" effect="blur:100" />
      <cld-transformation effect="brightness_hsb:-50" />
      <cld-transformation
        color="#FFFFFF"
        :overlay="{
          fontFamily: 'Neucha',
          fontSize: 100,
          fontWeight: 'bold',
          text: message,
          textAlign: 'center',
        }"
        width="1300"
        crop="fit"
      />
      <cld-transformation flags="layer_apply" />
      <cld-transformation
        color="#FFFFFF"
        :overlay="{
          fontFamily: 'Dancing Script',
          fontSize: 50,
          fontWeight: 'bold',
          text: `from ${name}`,
        }"
      />
      <cld-transformation
        flags="layer_apply"
        gravity="center"
        x="450"
        y="350"
      />
    </cld-image>

    <div class="mt-10">
      <h5>Shareable link</h5>
      <input
        disabled
        :value="url"
        class="w-full lg:w-2/5 h-10 border-[#B7B3B3] border rounded-sm p-2 mr-4"
      />
      <button
        class="bg-gray-600 py-2 px-6 rounded-[5px] text-white font-semibold"
        @click="handleCopyToClip"
      >
        {{ copy }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    message: { type: String, required: true },
    name: { type: String, required: true },
    publicId: { type: String, required: true },
  },

  data() {
    return {
      url: '',
      copy: 'Copy File',
    }
  },

  methods: {
    handleCopyToClip() {
      console.log(this.$refs)
      navigator.clipboard
        .writeText(this.url)
        .then(() => (this.copy = 'Copied!'))
        .catch((err) => console.log('error copying to clipboard', err))
    },
  },

  mounted() {
      console.log(this.$refs.ref.$el)
  },
}
</script>
