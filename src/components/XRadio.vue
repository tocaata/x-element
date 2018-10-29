<template>
  <label :class="{ 'is-bordered': border, 'is-checked': checked}" class="x-radio">
    <input type="radio"
           :value="label"
           :checked="checked"
           class="x-radio__input"
           :class="{ 'is-checked': checked }"
           :name="name"
           :disabled="disabled"
           @change="change"/>
    <span class="x-radio__label">
      <slot></slot>
    </span>
  </label>
</template>

<script>
  export default {
    name: 'XRadio',
    data() {
      return {
      };
    },
    props: {'value': String, 'label': String, 'disabled': Boolean, 'name': String, 'border': Boolean},
    computed: {
      checked() {
        return this.value === this.label;
      }
    },
    methods: {
      change(event) {
        this.$emit('input', event.target.value);
      }
    }
  }
</script>

<style type="text/css" scoped>
  .x-radio {
    color: #606266;
    font-weight: 500;
    line-height: 1;
    position: relative;
    cursor: pointer;
    display: inline-block;
    white-space: nowrap;
    outline: none;
    font-size: 14px;
  }

  .x-radio.is-bordered {
    padding: 12px 20px 0 10px;
    border-radius: 4px;
    border: 1px solid #dcdfe6;
    box-sizing: border-box;
    height: 40px;
  }

  .x-radio.is-bordered.is-checked {
    border-color: #409eff;
  }

  .x-radio__input {
    white-space: nowrap;
    cursor: pointer;
    outline: none;
    display: inline-block;
    line-height: 1;
    position: relative;
    vertical-align: middle;
  }

  .x-radio__label {
    font-size: 14px;
    padding-left: 10px;
  }

  .x-radio__input.is-checked+.x-radio__label {
    color: #409eff;
  }
</style>
