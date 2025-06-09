<template>
  <p class="mb-3 md:mb-7 fadein-left fadeins-1">{{ displayedText }}</p>
</template>

<script>
export default {
  props: {
    text: String,
    speed: {
      type: Number,
      default: 30
    }
  },
  data() {
    return {
      displayedText: '',
      characters: '!<>-_\\/[]{}—=+*^?#________'
    };
  },
  mounted() {
    this.startDecryption();
  },
  methods: {
    startDecryption() {
      const finalText = this.text;
      let i = 0;
      const interval = setInterval(() => {
        const placeholder = finalText
          .split('')
          .map((char, index) => {
            if (index < i) return finalText[index];
            return this.characters[Math.floor(Math.random() * this.characters.length)];
          })
          .join('');
        this.displayedText = placeholder;
        i++;
        if (i > finalText.length) clearInterval(interval);
      }, this.speed);
    }
  }
};
</script>

<style scoped>
.fadein-left {
  opacity: 0;
  animation: fadeInLeft 0.5s ease-out forwards;
}
@keyframes fadeInLeft {
  0% {
    opacity: 0;
    transform: translateX(100%);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}
</style>
