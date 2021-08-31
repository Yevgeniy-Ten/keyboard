<template>
  <div class="keyboard">
    <Keys
      :type="type"
      v-for="row_id in Object.keys(keys)"
      :upperMode="upperMode"
      :onClickHandler="onClickHandler"
      :key="row_id"
      :keys="keys[row_id]"
    />
  </div>
</template>

<script>
import Keys from "./Keys";

export default {
  name: "Keyboard",
  props: {
    onClickHandler: Function,
    upperMode: Boolean,
    type: String,
  },
  components: {
    Keys,
  },
  data() {
    return {
      // keys: {
      //   0: [
      //     {
      //       value: 1,
      //     },
      //     {
      //       value: 2,
      //     },
      //     {
      //       value: 3,
      //     },
      //   ],
      //   1: [
      //     {
      //       value: 4,
      //     },
      //     {
      //       value: 5,
      //     },
      //     {
      //       value: 6,
      //     },
      //   ],
      //   2: [
      //     {
      //       value: 7,
      //     },
      //     {
      //       value: 8,
      //     },
      //     {
      //       value: 9,
      //     },
      //   ],
      //   3: [
      //     {
      //       value: "backspace",
      //     },
      //     {
      //       value: 0,
      //     },
      //     {
      //       value: "enter",
      //     },
      //   ],
      // },
      keys: {
        0: [
          {
            upValue: "!",
            value: 1,
          },
          {
            upValue: "@",
            value: 2,
          },
          {
            upValue: "#",
            value: 3,
          },
          {
            upValue: "$",
            value: 4,
          },
          {
            upValue: "%",
            value: 5,
          },
          {
            upValue: "^",
            value: 6,
          },
          {
            upValue: "&",
            value: 7,
          },
          {
            upValue: "*",
            value: 8,
          },
          {
            upValue: "(",
            value: 9,
          },
          {
            upValue: ")",
            value: 0,
          },
        ],
        1: [
          {
            value: "q",
          },
          {
            value: "w",
          },
          {
            value: "e",
          },
          {
            value: "r",
          },
          {
            value: "t",
          },
          {
            value: "y",
          },
          {
            value: "u",
          },
          {
            value: "i",
          },
          {
            value: "o",
          },
          {
            value: "p",
          },
        ],
        2: [
          {
            value: "a",
          },
          {
            value: "s",
          },
          {
            value: "d",
          },
          {
            value: "f",
          },
          {
            value: "g",
          },
          {
            value: "h",
          },
          {
            value: "j",
          },
          {
            value: "k",
          },
          {
            value: "l",
          },
          {
            value: "_",
          },
        ],
        3: [
          {
            value: "l_shift",
          },
          {
            value: "z",
          },
          {
            value: "x",
          },
          {
            value: "c",
          },
          {
            value: "v",
          },
          {
            value: "b",
          },
          {
            value: "n",
          },
          {
            value: "m",
          },
          {
            value: ".",
          },
          {
            value: "backspace",
          },
        ],
        4: [
          {
            value: "vector_l",
          },
          {
            value: "vector_r",
          },
          {
            value: "space",
          },
          {
            value: "-",
          },
          {
            value: "enter",
          },
        ],
      },
    };
  },
};
</script>

<style scoped lang="scss">
.keyboard {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #191c22;
  padding: 26px;
  border-radius: 14px 14px 0 0;
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>
