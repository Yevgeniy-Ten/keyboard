<template>
  <div v-if="type !== 'number'" class="row">
    <div
      class="col"
      @mousedown="
        () =>
          onClickHandler(
            upperMode ? symbol.upValue || symbol.value : symbol.value,
            'run'
          )
      "
      @mouseup="
        () =>
          onClickHandler(
            upperMode ? symbol.upValue || symbol.value : symbol.value,
            'stop'
          )
      "
      v-for="symbol in keys"
      :key="symbol.value"
      :class="{
        'col-6': symbol.value === 'space',
        'col-2': symbol.value === 'enter',
        isEnter: symbol.value === 'enter',
        active: upperMode && symbol.value === 'l_shift',
        'col-light-dark': typeof symbol.value === 'number',
      }"
    >
      <span class="upper-span" v-if="symbol.upValue">{{ symbol.upValue }}</span>
      <span v-if="symbol.value === 'l_shift'" class="l_shift" />
      <span v-else-if="symbol.value === 'backspace'" :class="symbol.value" />
      <span v-else-if="symbol.value === 'vector_l'" :class="symbol.value" />
      <span v-else-if="symbol.value === 'vector_r'" :class="symbol.value" />
      <span v-else-if="symbol.value === 'space'" :class="symbol.value" />
      <span v-else-if="symbol.value === 'enter'" :class="symbol.value" />
      <span :class="{ 'text-upper': upperMode }" v-else>{{
        symbol.value
      }}</span>
    </div>
  </div>
  <div v-else class="row">
    <div
      class="col col-num"
      @mousedown="() => onClickHandler(symbol.value, 'run')"
      @mouseup="() => onClickHandler(symbol.value, 'stop')"
      v-for="symbol in keys"
      :class="{
        isEnter: symbol.value === 'enter',
        'col-light-dark': symbol.value === 'backspace',
      }"
      :key="symbol.value"
    >
      <span v-if="symbol.value === 'backspace'" :class="symbol.value" />
      <span v-else-if="symbol.value === 'enter'" :class="symbol.value" />
      <span v-else>{{ symbol.value }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    type: String,
    keys: Array,
    onClickHandler: Function,
    upperMode: Boolean,
  },
};
</script>
<style scoped lang="scss">
.row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;

  &:first-child > .col {
    background-color: #343c45;

    &:active {
      background-color: #ffffff;
      color: #3c4043;
    }
  }
}

.col {
  box-sizing: border-box;
  background-color: #2a3139;
  border-radius: 8px;
  flex-basis: 6%;
  min-height: 90px;
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  font-weight: 500;
  font-size: 33px;
  cursor: pointer;
  position: relative;

  &-light-dark {
    background-color: #343c45;
  }

  &-num {
    flex-basis: 30%;
  }

  &.active {
    background-color: #ffffff;
  }

  &-2 {
    flex-basis: 16.5%;
  }

  &-6 {
    flex-basis: 47.6%;
  }

  &:active {
    background-color: #ffffff;
    color: #3c4043;
  }
}

.isEnter {
  background-color: #3a4b5d;
}

.upper-span {
  margin-left: auto;
  margin-right: 10px;
  display: inline-block;
  color: #bdc1c6;

  & ~ span {
    margin-right: 12px;
    margin-bottom: 6px;
  }
}

.text-upper {
  text-transform: uppercase;
}

.l_shift {
  background: url("./l_shift-i.png") no-repeat center / contain;
  padding: 14px;
}

.backspace {
  background: url("./backspace-i.svg") no-repeat center / contain;
  padding: 14px;
}

.vector_l {
  background: url("./left-kar-i.svg") no-repeat center / contain;
  padding: 14px;
}

.vector_r {
  background: url("./right-car-i.svg") no-repeat center / contain;
  padding: 14px;
}

.space {
  background: url("./space-i.svg") no-repeat center / contain;
  padding: 14px;
}

.enter {
  background: url("./enter-i.svg") no-repeat center / contain;
  padding: 14px;
}
</style>
