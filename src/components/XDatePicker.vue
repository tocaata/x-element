<template>
  <div style="display: inline-flex; position: relative">
    <p class="control has-icons-left has-icons-right" ref="control">
      <span class="icon is-small is-left" style="pointer-events: auto; cursor: pointer;">
        <i class="far fa-calendar-alt"></i>
      </span>
      <input type="text" :value="value" class="input" placeholder="选择日期" @click.stop="togglePicker" />
      <span ref="clear" class="icon is-small is-right" style="pointer-events: auto; cursor: pointer;" v-show="showClear" @click.stop="clear">
        <i class="far fa-times-circle"></i>
      </span>
    </p>
    <div class="box" v-show="showPicker" data-picker>
      <div data-picker-header>
        <button type="button" class="pre-btn" @click.stop="preYear"><<</button>
        <button type="button" class="pre-btn" @click.stop="preMonth"><</button>
        <span>{{ dayPt.year() }}年</span>
        <span>{{ dayPt.month() + 1 }}月</span>
        <button type="button" class="next-btn" @click.stop="nextYear">>></button>
        <button type="button" class="next-btn" @click.stop="nextMonth">></button>
      </div>
      <table class="table" @click.stop="pickDate">
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
                :data-date="dateString(date)"
                :class="{ 'disabled-cell': date.disabled, 'today': isToday(date), 'chose': dateString(date) === pickedDate }">
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
    props: {
      value: String,
      clearable: Boolean
    },
    data() {
      return {
        dayPt: moment(),
        today: moment(),
        showPicker: false,
        pickedDate: this.value,
        showClear: false
      }
    },
    mounted() {
      document.addEventListener('click', (e) => {
        this.showPicker = false;
      });
      if (this.clearable) {
        this.$refs.control.addEventListener('mouseover', (e) => {
          if (!this.showClear)
            this.showClear = true;
        });
        this.$refs.control.addEventListener('mouseout', (e) => {
          if (this.showClear)
            this.showClear = false;
        });
      }
    },
    computed: {
      tableList() {
        return [];
      },
      dayList() {
        const month = this.dayPt.clone().date(15).month();
        const ptr = this.dayPt.clone().date(1).day(0);
        const ret = [[],[],[],[],[],[]];

        for (let i = 0; i < 42; i++) {
          ret[Math.floor(i / 7)].push({year: ptr.year(), month: ptr.month() + 1, date: ptr.date(), disabled: ptr.month() !== month});
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
    watch: {
      pickedDate(newValue) {
        this.$emit('input', newValue);
      }
    },
    methods: {
      clear() {
        this.pickedDate = null;
        this.showPicker = false;
      },
      preYear() {
        this.dayPt = this.dayPt.clone().subtract(1, 'y');
      },
      preMonth() {
        this.dayPt = this.dayPt.clone().subtract(1, 'M');
      },
      nextYear() {
        this.dayPt = this.dayPt.clone().add(1, 'y');
      },
      nextMonth() {
        this.dayPt = this.dayPt.clone().add(1, 'M');
      },
      isToday(day) {
        return day.date === this.today.date() && day.month === (this.today.month() + 1) && day.year === this.today.year();
      },
      togglePicker() {
        this.showPicker = !this.showPicker;
      },
      pickDate(e) {
        let target = null;
        if (e.target.tagName === 'SPAN') {
          target = e.target.parentElement;
        } else {
          target = e.target;
        }
        this.pickedDate = target.dataset.date;
        this.showPicker = false;
      },
      dateString(day) {
        return `${day.year}-${day.month}-${day.date}`
      }
    }
  }
</script>

<style scoped>
  div[data-picker-header] button {
    border: 0;
    font-size: 1rem;
    outline: none;
    margin-bottom: 1rem;
  }

  div[data-picker-header] button:hover, div[data-picker-header] span:hover {
    cursor: pointer;
    color: #409eff;
  }

  div[data-picker-header] button.pre-btn {
    float: left;
  }

  div[data-picker-header] button.next-btn {
    float: right;
  }

  input.input {
    z-index: 1;
    width: 12rem;
    cursor: pointer;
    transition: all .3s;
    padding: 0 15px;
  }

  div.box[data-picker] td:hover {
    color: #409eff;
  }

  div.box[data-picker] {
    display: block;
    position: absolute;
    top: 32px;
    margin-top: 0.5rem;
    cursor: pointer;
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

  td.chose span {
    color: white;
    border-radius: 50%;
    border: 1px solid #409eff;
    background-color: #409eff;
  }
</style>
