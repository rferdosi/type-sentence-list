<template>
  <type-sentence-list :list="['Hi', 'How Are You?']" />
</template>

<script>
import TypeSentenceList from "./components/TypeSentenceList.vue";

export default {
  name: "App",
  components: {
    TypeSentenceList,
  },
};
</script>