<template>
  <div>{{ current }}</div>
</template>

<script>
export default {
  name: "TypeSentenceList",
  props: {
    list: Array,
  },
  data: () => ({
    currentSentenceIndex: 0,
    lastCharIndex: 0,
  }),
  mounted() {
    this.typeSentence();
  },
  computed: {
    currentText() {
      if (!this.list || !this.list.length) {
        return "";
      }
      return this.list[this.currentSentenceIndex];
    },
    current() {
      if (this.currentText) {
        return this.currentText.slice(0, this.lastCharIndex);
      }
      return "";
    },
  },
  methods: {
    eraseSentence() {
      this.interval = setInterval(() => {
        if (this.lastCharIndex === 0) {
          this.currentSentenceIndex = (this.currentSentenceIndex + 1) % this.list.length;
          clearInterval(this.interval);
          this.typeSentence();
        } else {
          this.lastCharIndex = this.lastCharIndex - 1;
        }
      }, 100);
    },
    typeSentence() {
      this.interval = setInterval(() => {
        if (this.lastCharIndex === this.currentText.length) {
          clearInterval(this.interval);
          this.eraseSentence();
        } else {
          this.lastCharIndex = this.lastCharIndex + 1;
        }
      }, 100);
    },
  },
};
</script>