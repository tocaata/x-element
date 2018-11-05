<template>
  <div style="display: inline-flex; position: relative">
    <input type="text" class="input" placeholder="选择日期" @click.stop="togglePicker" />
    <div class="box" v-show="showPicker" @click.stop="pickDate" data-picker>
      <table class="table">
        <tbody>
        <tr>
          <td>日</td>
          <td>一</td>
          <td>二</td>
          <td>三</td>
          <td>四</td>
          <td>五</td>
          <td>六</td>
        </tr>
        <tr v-for="list in dayList">
          <td v-for="date in list"
              :class="{ 'disabled-cell': date.disabled, 'today': isToday(date) }">
            <span>{{ date.date }}</span>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
  import moment from 'moment';

  export default {
    name: "XDatePicker",
    data() {
      const today = moment();
      return {
        today: {
          year: today.year(),
          month: today.month(),
          date: today.date()
        },
        showPicker: false
      }
    },
    mounted() {
      document.addEventListener('click', (e) => {
        this.showPicker = false;
      });
    },
    computed: {
      tableList() {
        return [];
      },
      dayList() {
        const today = moment();
        const month = today.month();
        const ptr = moment().date(1).day(0);
        const ret = [[],[],[],[],[],[]];
        for (let i = 0; i < 42; i++) {
          ret[Math.floor(i / 7)].push({year: ptr.year(), month: ptr.month(), date: ptr.date(), disabled: ptr.month() !== month});
          ptr.add(1, 'd');
        }
        return ret;
      },
      monthList() {
        1
      },
      yearList() {
        1
      }
    },
    methods: {
      isToday(day) {
        return day.date === this.today.date && day.month === this.today.month;
      },
      togglePicker() {
        console.log(this.showPicker);
        this.showPicker = !this.showPicker;
      },
      pickDate(e) {
        console.log(e.target);
      }
    }
  }
</script>

<style scoped>
  input.input {
    z-index: 1;
    width: 12rem;
    cursor: pointer;
    transition: all .3s;
    padding: 0 15px;
  }

  div.box[data-picker] {
    display: block;
    position: absolute;
    top: 32px;
    margin-top: 0.5rem;
  }

  table.table {
    font-size: 12px;
    font-weight: 700;
  }

  td.disabled-cell {
    color:hsl(0, 0%, 86%);
  }

  td.today {
    color: #409eff;
  }

  td span {
    display: block;
    width: 24px;
    height: 24px;
    text-align: center;
    line-height: 24px;
  }

  td span.choosed {
    color: white;
    border-radius: 50%;
    border: 1px solid #409eff;
    background-color: #409eff;
  }
</style>
