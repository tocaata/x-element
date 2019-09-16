<template>
  <div ref="container" class="box" id="abcd">
    <div class="header" @mousedown="handleMouseDown" @mouseup="handleMouseUp"></div>
    <slot class="content"></slot>
  </div>
</template>

<script>
  export default {
    name: "Movable",
    data() {
      return {
        mousePosition: [0, 0]
      };
    },
    mounted() {
      // window.addEventListener('mouseup', this.handleMouseUp)
      // window.addEventListener('keypress', this.handleKeyDown);
    },
    methods: {
      handleMouseDown(e) {
        // this.mousePosition = [e.layerX, e.layerY];
        window.addEventListener('mousemove', this.handleMouseMove);
      },

      handleMouseUp(e) {
        window.removeEventListener('mousemove', this.handleMouseMove);
      },
      handleMouseMove(e) {
        const container = this.$refs.container;
        // console.log(e);

        const offset = [e.movementX, e.movementY];
        let {offsetLeft, offsetTop} = container;
        container.style.left = `${offsetLeft + offset[0]}px`;
        container.style.top = `${offsetTop + offset[1]}px`;
      }
    }
  }
</script>

<style scoped>
.header {
  background-color: #409eff;
  height: 30px;
  cursor: move;
  border-radius: 6px 6px 0 0;
  box-shadow: 0 2px 3px rgba(10,10,10,.1), 0 0 0 1px rgba(10,10,10,.1);
  margin: -20px -20px 20px -20px;
}

.box {
  position: absolute;
  top: 50%;
  left: 20%;
  transform: translate(-50%, -50%);
  z-index: 20;
}
</style>
