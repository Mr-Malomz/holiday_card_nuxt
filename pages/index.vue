<template>
  <div class="p-10">
    <h1 class="text-3xl">Holiday Card Generator</h1>
    <header class="flex border-b-2 mt-7 mb-7">
      <NuxtLink
        to="#"
        class="text-base capitalize mr-8 pb-4"
        :class="
          tab === 'harvest'
            ? 'font-bold border-b-4 border-blue-600 text-blue-600'
            : 'text-gray-600'
        "
        @click.native="setTab('harvest')"
        >harvest month</NuxtLink
      >
      <NuxtLink
        to="#"
        class="text-base capitalize mr-8 pb-4"
        :class="
          tab === 'thanksgiving'
            ? 'font-bold border-b-4 border-blue-600 text-blue-600'
            : 'text-gray-600'
        "
        @click.native="setTab('thanksgiving')"
        >thanksgiving</NuxtLink
      >
      <NuxtLink
        to="#"
        class="text-base capitalize mr-8 pb-4"
        :class="
          tab === 'diwali'
            ? 'font-bold border-b-4 border-blue-600 text-blue-600'
            : 'text-gray-600'
        "
        @click.native="setTab('diwali')"
        >diwali</NuxtLink
      >
    </header>
    <form class="lg:w-2/5" @submit.prevent="handleSubmit">
      <section class="mb-6">
        <label className="block text-sm text-gray-600 mb-2">
          Select an image
        </label>
        <div v-if="tab === 'harvest'" class="flex items-center">
          <div
            v-for="item in harvest"
            :key="item.id"
            class="mr-2"
            :class="item.id === imageId ? 'border-blue-600 border-4' : ''"
            @click="handleSelectedImg(item.id, item.publicId)"
          >
            <cld-image :public-id="item.publicId">
              <cld-transformation crop="scale" width="80" height="80" />
            </cld-image>
          </div>
        </div>
        <div v-if="tab === 'thanksgiving'" class="flex items-center">
          <div
            v-for="item in thanksgiving"
            :key="item.id"
            class="mr-2"
            :class="item.id === imageId ? 'border-blue-600 border-4' : ''"
            @click="handleSelectedImg(item.id, item.publicId)"
          >
            <cld-image :public-id="item.publicId">
              <cld-transformation crop="scale" width="80" height="80" />
            </cld-image>
          </div>
        </div>
        <div v-if="tab === 'diwali'" class="flex items-center"> 
          <div
            v-for="item in diwali"
            :key="item.id"
            class="mr-2"
            :class="item.id === imageId ? 'border-blue-600 border-4' : ''"
            @click="handleSelectedImg(item.id, item.publicId)"
          >
            <cld-image :public-id="item.publicId">
              <cld-transformation crop="scale" width="80" height="80" />
            </cld-image>
          </div>
        </div>
        <p v-if="formData.error" class="text-sm text-red-500">
          Please select an image
        </p>
      </section>
      <div class="mb-6">
        <label class="block text-sm text-text-gray-600 mb-2">Message</label>
        <textarea
          v-model="formData.message"
          rows="4"
          required
          name="message"
          maxLength="{140}"
          class="w-full border-gray-600 border rounded-sm p-2"
        />
      </div>
      <div class="mb-6">
        <label class="block text-sm text-text-gray-600 mb-2">Name</label>
        <input
          v-model="formData.name"
          required
          name="name"
          class="w-full h-10 border-gray-600 border rounded-sm p-2"
        />
      </div>
      <button class="bg-blue-600 py-3 px-7 rounded-sm text-white font-semibold">
        Generate Card
      </button>
    </form>

    <div v-if="showCard" class="mt-10">
      <Card
        :message="formData.message"
        :name="formData.name"
        :publicId="formData.publicId"
      />
    </div>
  </div>
</template>

<script>
import harvest from '@/utils/harvest.json'
import thanksgiving from '@/utils/thanksgiving.json'
import diwali from '@/utils/diwali.json'

export default {
  data() {
    return {
      harvest,
      thanksgiving,
      diwali,
      tab: 'harvest',
      imageId: null,
      formData: {
        message: '',
        name: '',
        publicId: null,
        error: false,
      },
      showCard: false,
    }
  },

  methods: {
    setTab(tabName) {
      this.tab = tabName
    },

    handleSelectedImg(imgId, publicId) {
      this.imageId = imgId
      this.formData.publicId = publicId
      this.formData.error = false
      this.showCard = false
    },

    handleSubmit() {
      if (this.imageId) {
        this.showCard = true
      } else {
        this.formData.error = true
      }
    },
  },
}
</script>
