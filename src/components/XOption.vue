<template>
  <li class="dropdown-item" ref="the" :value="value" @click="handleClick">
    <span>{{label}}</span>
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
        this.$parent.$emit('input', this.value);
        console.log(this.$parent);
        // this.$emit('click', this.value);
        // event.target = this.$refs['the'];
      }
    }
  }
</script>

<style scoped>
  .dropdown-item:hover {
    background-color: #f5f5f5;
    color: #0a0a0a;
  }

  li.dropdown-item {
    padding-right: 3rem;
    text-align: left;
    white-space: nowrap;
    width: 100%;
    cursor: pointer;
  }
</style>
