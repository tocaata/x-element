<template>
  <div class="box">
    <table class="table">
      <thead>
        <tr>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(list, rowIndex) in dayList">
          <td v-for="(col, colIndex) in list"
              :class="{ 'disabled-cell': col.disabled }">
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: "XDatePicker",
    data() {
      return {
        current: {
          year: 1970,
          month: 1,
          day: 1
        }
      }
    },
    computed: {
      tableList() {
        return [];
      },
      dayList() {
        const days = [];
        
      },
      monthList() {
        1
      },
      yearList() {
        1
      }
    }
  }
</script>

<style scoped>
  td.disabled-cell {
    color:hsl(0, 0%, 86%);
  }

</style>
