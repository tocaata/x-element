<template>
  <table class="table">
    <thead>
      <tr>
        <slot></slot>
      </tr>
    </thead>
    <tbody>
      <tr v-for="line in props">
        <slot :prop="col" v-for="col in Object.values(line)">
          aaaa
        </slot>
      </tr>
    </tbody>
  </table>
</template>

<script>
  export default {
    name: "XTable",
    props: {
      data: Array
    },
    data() {
      1;
    },
    methods: {
    }
  }
</script>

<style scoped>

</style>
