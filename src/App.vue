<template>
  <button @click="learnVue">Open</button>
  <Popup ref="confirmationPopup">
    Do you really want to learn the right approaches to designing systems in Vue?
    <template #actions="{ confirm }">
        Write
      <input :placeholder="$options.CONFIRMATION_TEXT" v-model="confirmation">
      &nbsp;
      <button @click="confirm" :disabled="!isConfirmationCorrect">Ok</button>
    </template>
  </Popup>
</template>
<script>
import Popup from "./components/Popup";
export default {
  components: {
    Popup
  },
  CONFIRMATION_TEXT: "I confirm",
  data() {
    return {
      confirmation: ''
    }
  },
  computed: {
    isConfirmationCorrect() {
      return this.confirmation === this.$options.CONFIRMATION_TEXT
    }
  },
  methods: {
    async learnVue() {
      this.confirmation = '';
      const popupResult = await this.$refs.confirmationPopup.open();

      if (popupResult) {
        alert("Confirmed");
      }
    }
  }
}
</script>
