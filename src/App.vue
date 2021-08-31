<template>
  <input
      v-model="inputTxT"
      ref="inputTxT"
      @focus="onFocusToggler"
      type="text"
  />
  <Keyboard
      :upperMode="upperMode"
      :onClickHandler="onClickHandler"
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
    inputTxT() {
      this.setCaretPosition()
    }
  },
  methods: {
    onFocusToggler() {
      if (!this.isShowed) {
        this.isShowed = true;
      }
    },
    onUpperMode() {
      this.upperMode = !this.upperMode;
    },
    setCaretPosition() {
      const inputRef = this.$refs.inputTxT;
      if (inputRef.setSelectionRange) {
        inputRef.focus()
        console.log("kek")
        inputRef.setSelectionRange(this.caretPosition, this.caretPosition);
      } else if (inputRef.createTextRange) {
        const range = inputRef.createTextRange();
        range.collapse(true);
        range.moveEnd("character", this.caretPosition);
        range.moveStart("character", this.caretPosition);
        range.select();
      }
    },
    onClickHandler(key, event) {
      if (event === "run") {
        if (key === "backspace") {
          this.inputTxT = this.inputTxT.slice(0, -1);
          if (this.caretPosition > 0) {
            this.caretPosition -= 1;
          }
          const intervalId = setInterval(() => {
            this.repeatTime -= 50;
            this.inputTxT = this.inputTxT.slice(0, -1);
            if (this.repeatTime < 0) {
              this.repeatTime = 0;
            }
            if (this.caretPosition > 0) {
              this.caretPosition -= 1;
            }
            this.intervalIdx.push(intervalId);
          }, this.repeatTime);
        }
      } else {
        if (event === "stop") {
          this.isRepeat = false;
          this.intervalIdx.forEach((el) => clearInterval(el));
          this.repeatTime = 400;
        }
        if (key.toString().length === 1) {
          const inputTxtSplitter = this.inputTxT.split("");
          inputTxtSplitter.splice(
              this.caretPosition,
              0,
              this.upperMode ? key.toString().toUpperCase() : key
          );
          this.inputTxT = inputTxtSplitter.join("");
          this.caretPosition += 1;
        } else {
          if (key === "l_shift") {
            this.onUpperMode();
          } else if (key === "backspace") {
            this.inputTxT = this.inputTxT.slice(0, -1);
            if (this.caretPosition > 0) {
              this.caretPosition -= 1;
            }
          } else if (key === "space") {
            this.inputTxT += " ";
            this.caretPosition += 1;
          } else if (key === "vector_l" || key === "vector_r") {
            if (key === "vector_l" && this.caretPosition > 0) {
              this.caretPosition -= 1;
            } else if (key === "vector_r" && this.caretPosition < this.inputTxT.length) {
              this.caretPosition += 1;
            }
          }
        }
      }
    },
  },
  data() {
    return {
      isShowed: false,
      upperMode: false,
      inputTxT: "",
      isRepeat: false,
      intervalIdx: [],
      repeatTime: 3000,
      caretPosition: 0,
    };
  },
};
</script>
