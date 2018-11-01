<template>
  <div class="dropdown" :class="{ 'is-active': active }">
    <div class="dropdown-trigger">
      <button class="button" aria-haspopup="true" @click="handleButtonClick" @mouseover="innerValue ? (icon = 'delete') : ''" @mouseout="icon = 'down'">
        <span>{{innerValue}}</span>
        <span class="icon is-small" @click.stop="handleDelete" icon>
          <i class="fas" :class="{ 'fa-angle-down': icon === 'down', 'fa-times-circle': icon === 'delete'}" aria-hidden="true"></i>
        </span>
      </button>
    </div>
    <div class="dropdown-menu" role="menu">
      <div class="dropdown-content">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'XSelect',
    props: {
      value: [String, Number]
    },
    data() {
      return {
        innerValue: this.value,
        active: false,
        icon: 'down'
      };
    },
    mounted() {
      this.$on('click', (value) => this.handleOptionClick(value));
    },
    methods: {
      handleButtonClick(event) {
        this.active = !this.active;
      },
      handleDelete(e) {
        if (this.icon === 'delete') {
          this.innerValue = null;
          this.active = false;
        }
      },
      handleOptionClick(value) {
        this.active = !this.active;
        this.innerValue = value;
        this.$emit('input', value);
      }
    }
  }
</script>

<style scoped>
  .button {
    min-width: 12rem;
    justify-content: normal;
  }

  .icon[icon] {
    position: absolute;
    right: 1rem;
  }
</style>
