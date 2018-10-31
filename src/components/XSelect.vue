<template>
  <div class="dropdown is-active">
    <div class="dropdown-trigger">
      <button class="button" aria-haspopup="true" aria-controls="dropdown-menu">
        <span>{{value}}</span>
        <span class="icon is-small">
        <i class="fas fa-angle-down" aria-hidden="true"></i>
      </span>
      </button>
    </div>
    <div class="dropdown-menu" id="dropdown-menu" role="menu">
      <div class="dropdown-content" @input="handleClick">
        <slot :onclick="(event) => { handleClick(event); }"></slot>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'XSelect',
    props: {
      value: [String, Number, undefined],
      abc: [String, undefined]
    },
    data() {
      return {
      };
    },
    mounted() {
    },
    methods: {
      handleClick(event) {
        // console.log('event', event);
        console.log(event);
        // debugger
        this.$emit('input', event.target.value);
      }
    }
  }
</script>

<style scoped>

</style>
