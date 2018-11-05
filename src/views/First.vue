<template>
  <div>
    <div>
      Step: {{step}}
      select: {{selectData}}
    </div>
    <XRadio v-model="myData" label="1">你好</XRadio>
    <XRadio border v-model="myData" label="2">你也好</XRadio>
    <br/>
    <XInputNumber v-model="step" name="step" :min="-12" :max="15" :step="1" style="margin-top: 10px"></XInputNumber>
    <XSelect style="margin-top: 10px" v-model="selectData" placeholder="请选择" clearable multiple>
      <XOption v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
      </XOption>
    </XSelect>
    <br/>
    <XDatePicker style="margin: 1rem 1rem"></XDatePicker>
  </div>
</template>

<script>
  import XRadio from '../components/XRadio';
  import XInputNumber from '../components/XInputNumber';
  import XSelect from '../components/XSelect';
  import XOption from '../components/XOption';
  import XDatePicker from '../components/XDatePicker';

  export default {
    name: 'First',
    components: {XInputNumber, XRadio, XSelect, XOption, XDatePicker},
    data() {
      return {
        myData: null,
        step: 2,
        selectData: null,
        options: [{
          value: '黄金糕',
          label: '黄金糕'
        }, {
          value: '双皮奶',
          label: '双皮奶'
        }, {
          value: '蚵仔煎',
          label: '蚵仔煎'
        }, {
          value: '龙须面',
          label: '龙须面'
        }, {
          value: '北京烤鸭',
          label: '北京烤鸭'
        }]
      }
    },
    watch: {
      selectData(newValue) {
        console.log(newValue);
      }
    }
  }
</script>

<style scoped>

</style>
