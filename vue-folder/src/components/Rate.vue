<template>
  <div>
    <h1>Reacción de los usuarios</h1>
    <vue-feedback-reaction v-model="selectedReaction" @change="onReactionChange"></vue-feedback-reaction>
    <p>Has seleccionado la reacción: {{ selectedReaction }}</p>
  </div>
</template>

<script>
import VueFeedbackReaction from 'vue-feedback-reaction';

export default {
  components: {
    VueFeedbackReaction
  },
  data() {
    return {
      selectedReaction: null
    };
  },
  methods: {
    onReactionChange(newReaction) {
      console.log('Nueva reacción seleccionada:', newReaction);
    }
  }
};
</script>
