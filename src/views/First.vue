<template>
  <div>
    <div>
      Step: {{step}}
    </div>
    <XRadio v-model="myData" label="1">你好</XRadio>
    <XRadio border v-model="myData" label="2">你也好</XRadio>
    <br/>
    <XInputNumber v-model="step" name="step" :min="-12" :max="15" :step="1" style="margin-top: 10px"></XInputNumber>
    <XSelect style="margin-top: 10px" v-model="selectData">
      <x-options v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
      </x-options>
    </XSelect>
  </div>
</template>

<script>
  import XRadio from '../components/XRadio';
  import XInputNumber from '../components/XInputNumber';
  import XSelect from '../components/XSelect';

  export default {
    name: 'First',
    components: {XInputNumber, XRadio, XSelect},
    data() {
      return {
        myData: null,
        step: 2,
        selectData: null,
        options: [{
          value: '选项1',
          label: '黄金糕'
        }, {
          value: '选项2',
          label: '双皮奶'
        }, {
          value: '选项3',
          label: '蚵仔煎'
        }, {
          value: '选项4',
          label: '龙须面'
        }, {
          value: '选项5',
          label: '北京烤鸭'
        }]
      }
    }
  }
</script>

<style scoped>

</style>
