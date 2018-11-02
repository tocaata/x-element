<template>
  <li class="dropdown-item"
      :class="{ 'option-highlight': highlight }"
      :value="value"
      @click.prevent.stop="handleClick">
    <span>{{ label }}</span>
  </li>
</template>

<script>
  export default {
    name: 'XOption',
    props: {
      label: String,
      onclick: Function,
      value: [String, Number]
    },
    methods: {
      handleClick(event) {
        // event.preventDefault();
        // event.stopPropagation();
        this.$parent.$emit('click', this.value);
      }
    },
    computed: {
      highlight() {
        return this.$parent.innerValue === this.value || (this.$parent.innerValue && this.$parent.innerValue.includes(this.value));
      }
    }
  }
</script>

<style scoped>
  .dropdown-item:hover {
    background-color: #f5f5f5;
    color: #0a0a0a;
  }

  .option-highlight {
    color: #409eff;
  }

  li.dropdown-item {
    padding-right: 3rem;
    text-align: left;
    white-space: nowrap;
    width: 100%;
    cursor: pointer;
  }
</style>
