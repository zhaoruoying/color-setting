<template>
  <label
    class="radio"
    :class="{ 'is-checked': model === label }"
    role="radio"
  >
    <span class="radio_input"
      :class="{
        'is-checked': model === label
      }"
    >
      <span class="radio_icon"></span>
      <input
        ref="radio"
        :value="label"
        type="radio"
        v-model="model"
        @change="handleChange"
      >
    </span>
    <span class="radio_label" @keydown.stop>
      <slot></slot>
      <template v-if="!$slots.default">{{label}}</template>
    </span>
  </label>
</template>
<script>
  export default {
    name: 'Radio',
    props: {
      value: {},
      label: {},
      name: String
    },

    data() {
      return {
        focus: false
      };
    },
    computed: {
      model: {
        get() {
          return this.value;
        },
        set(val) {
          this.$emit('input', val);
          this.$refs.radio && (this.$refs.radio.checked = this.model === this.label);
        }
      }
    },

    methods: {
      handleChange() {
        this.$nextTick(() => {
          this.$emit('change', this.model);
        });
      }
    }
  };
</script>
<style lang="scss" scoped>
.radio {
  display: inline-flex;
  margin-right: 27px;
  align-items: center;
  .radio_icon {
    border: 1px solid #47a1dd;
    border-radius: 100%;
    width: 12px;
    height: 12px;
    background-color: #fff;
    position: relative;
    cursor: pointer;
    display: inline-block;
    box-sizing: border-box;
  }
  .is-checked {
    .radio_icon {
      background: #38a7f0 url('../../assets/checked.png') no-repeat  1px center;
      background-size: 8px;
      border-color: #38a7f0;
    }
  }
  .radio_icon::after {
    background-color: #38a7f0;
  }
  .radio_input {
    margin-right:4px;
    display: flex;
    align-items: center;
    input {
      opacity: 0;
      outline: none;
      position: absolute;
      z-index: -1;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      margin: 0;
    }
  }
}
.radio:last-child {
  margin: 0;
}
</style>