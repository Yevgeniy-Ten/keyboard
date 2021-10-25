<template>
  <input
    v-model="inputTxT"
    ref="inputTxT"
    @focus="onFocusToggler"
    type="text"
  />
  <Keyboard
    @onChange="onChange"
    :caretPosition="caretPosition"
    :inputTxT="inputTxT"
    v-if="isShowed"
  />
</template>

<style lang="scss"></style>

<script>
import Keyboard from "./components/Keyboard";

export default {
  components: {
    Keyboard,
  },
  watch: {
    caretPosition() {
      this.$nextTick(() => {
        this.setCaretPosition();
      });
    },
  },
  methods: {
    onFocusToggler() {
      if (!this.isShowed) {
        this.isShowed = true;
      }
    },
    setCaretPosition() {
      const inputRef = this.$refs.inputTxT;
      if (inputRef.setSelectionRange) {
        inputRef.focus();
        inputRef.setSelectionRange(this.caretPosition, this.caretPosition);
      }
    },
    onChange(value, position) {
      this.inputTxT = value;
      this.caretPosition = position;
    },
  },
  data() {
    return {
      caretPosition: 0,
      inputTxT: "",
      isShowed: false,
    };
  },
};
</script>
