<template>
  <div class="w-full md:w-3/5 h-20 mx-auto md:mt-5">
    <div class="bg-white rounded-xl mx-3 p-5 md:p-10 md:mx-0">
      <div>
        <h1 class="text-xl md:text-4xl text-black text-left font-bold leading-relaxed">{{ title }}</h1>
        <div class="mt-3 text-left text-gray-800 text-sm">Published at <span>{{ date }}</span></div>
        <div class="h-[2px] w-20 my-5 md:my-10 bg-[#ffdb70] md:w-1/3 aos-init aos-animate mr-2"></div>
        <div>
          <div class="relative w-full" style="padding-top: 50%;">
            <img :src="image" class="absolute top-0 left-0 rounded-lg w-full h-full object-cover" alt="Thumbnail">
          </div>
        </div>
        <div class="text-left text-black mt-8" v-html="content"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      title: '',
      image: '',
      date: '',
      content: '',
    }
  },
  mounted() {
    this.getDetails();
  },
  methods: {
    async getDetails() {
      const id = this.$route.params.id;
      try {
        const response = await axios.get(`https://domainmu.com/api/posts/${id}`);
        const data = response.data;
        this.title = data.title;
        this.image = data.image;
        this.date = data.date;
        this.content = data.content;
      } catch (error) {
        console.error('Gagal mengambil detail artikel:', error);
      }
    }
  }
}
</script>

<style scoped></style>
