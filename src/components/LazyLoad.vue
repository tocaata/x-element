<template>
  <div ref="img" :style="{ height, width }">
    <img ref="source" :src="imageSrc">
  </div>
</template>

<script>
  export default {
    name: "LazyLoad",
    props: {
      src: String,
      height: [String, Number],
      width: [String, Number]
    },
    data() {
      return {
        imageSrc: '',
      }
    },
    mounted() {
      const interval = setInterval(() => {
        const scrollTop = window.pageYOffset;
        const viewPortSize = window.innerHeight || document.documentElement.clientHeight;

        if (scrollTop + viewPortSize > this.getOffsetTop(this.$refs.img) + 100) {
          this.imageSrc = this.src;
          clearInterval(interval);
        }
      }, 500);
    },
    methods: {
      getOffsetTop(ele) {
        let offset = ele.offsetTop;
        while(ele = ele.offsetParent) {
          offset += ele.offsetTop;
        }
        return offset;
      }
    }
  }
</script>

<style scoped>

</style>
