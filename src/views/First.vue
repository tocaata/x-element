<template>
  <div>
    <div>
      Step: {{step}}
      select: {{selectData}}
      Date: {{date}}
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
    <XDatePicker clearable v-model="date" style="margin: 1rem 1rem"></XDatePicker>
    <x-movable v-model="sortableData">
      <div slot-scope="scope" style="width: 100px; border: 1px solid red;">{{ scope.item.value }}</div>
    </x-movable>

    <movable style="width: 500px">
      <p>
        习近平称赞阿罗约和索托是中国人民的老朋友、好朋友，赞赏两位议长长期以来为中菲友好所做大量工作。习近平指出，近年来，中菲关系焕发新
        的活力，实现了由转圜、巩固到提升的跨越式发展，为两国人民带来福祉，促进了地区和平稳定。昨天，我同杜特尔特总统一致决定建立中菲全面
        战略合作关系，更好引领两国关系发展。我们要沿着这一正确道路继续大步向前，深化务实合作，夯实双边关系物质基础，加强人文交流，筑牢双
        边关系民意基础，妥处南海问题，坚持双边关系发展正确方向，做共同发展的好邻居、好伙伴。
      </p>
    </movable>
    <!--<XTable :data="students">-->
      <!--<XTableColumn prop="name"></XTableColumn>-->
    <!--</XTable>-->
    <div class="flex-div" style="position: absolute; top: 1000px;">
      <lazy-load class="middle-div" :src="require(`@/assets/地图2扩大范围.png`)" width="300px" height="200px"></lazy-load>
      <lazy-load class="middle-div" :src="require(`@/assets/picture1.jpg`)" width="600px" height="400px"></lazy-load>
    </div>
  </div>
</template>

<script>
  import XRadio from '../components/XRadio';
  import XInputNumber from '../components/XInputNumber';
  import XSelect from '../components/XSelect';
  import XOption from '../components/XOption';
  import XDatePicker from '../components/XDatePicker';
  import XTable from '../components/XTable';
  import XTableColumn from '../components/XTableColumn';
  import LazyLoad from '../components/LazyLoad';
  import Movable from '../components/Movable';
  import XMovable from '../components/XMovable';

  export default {
    name: 'First',
    components: {XTable, XTableColumn, XInputNumber, XRadio, XSelect, XOption, XDatePicker, LazyLoad, Movable, XMovable},
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
        }],
        date: null,
        students: [
          { name: '王磊' },
          { name: '张帆' }
        ],
        sortableData: [
          { key: 1, value: '1' },
          { key: 2, value: '2' },
          { key: 3, value: '3' },
          { key: 4, value: '4' }
        ]
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
  div.flex-div {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    width: 100%;
  }

  .middle-div {
  }
</style>
