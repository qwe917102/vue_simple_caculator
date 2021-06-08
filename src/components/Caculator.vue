<template>
  <div class="caculator align-items-center row mx-auto col-10">
    <input class="px-0 col-12 py-3 text-end" v-model="current" type="number" readonly>
    <div class="number-btn row m-0 col-9 p-0">
      <div @click="resetCurrent()" class="btn btn-outline-primary col-12 px-2">C</div>
      <div v-for="(n, index) in 9" :key="index" @click="append(n)" class="btn btn-outline-primary col-4 px-2">{{ n }}</div>
      <div @click="append(0)" class="btn btn-outline-primary col-12 px-2">0</div>
    </div>
    <div v-if="calculatingSigns" class="number-btn row m-0 col-3 p-0">
      <div @click="plus()" class="btn btn-outline-primary col-12 px-0">+</div>
      <div @click="minus()" class="btn btn-outline-primary col-12 px-0">-</div>
      <div @click="multiply()" class="btn btn-outline-primary col-12 px-0">x</div>
      <div @click="divid()" class="btn btn-outline-primary col-12 px-0">÷</div>
      <div @click="equal()" class="btn btn-outline-primary col-12 px-0">=</div>
      <!-- <div v-for="(item, index) in calculatingSigns" :key="index"
        class="btn btn-outline-primary col-12 px-0" :value="item.type">{{ item.show }}</div> -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'caculator',
  data() {
    return {
      current: '0',
      previous: '',
      operator: null,
      // 確認按下（下一個）數字開關
      operatorClicked: false,
      calculatingSigns: [
        {
          type: 'plus',
          sign: '+',
          show: '+'
        },
        {
          type: 'minus',
          sign: '-',
          show: '-'
        },
        {
          type: 'multiply',
          sign: '*',
          show: 'x'
        },
        {
          type: 'divid',
          sign: '/',
          show: '÷'
        },
        {
          type: 'equal',
          sign: '=',
          show: '='
        },
      ],
    };
  },
  methods: {
    // 重置變數
    resetCurrent() {
      this.current = '0';
      this.previous = '';
      this.operatorClicked = false;
      this.operator = null;
    },
    // 輸入數字
    append(number) {
      // 如果已點選任何運算子，則清空目前的值
      if (this.operatorClicked) {
        this.current = '0';
      }
      this.operatorClicked = false;
      this.current = Number(this.current) === 0 ? `${number}` : `${this.current}${number}`;
    },
    // 加法
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    // 減法
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    // 乘法
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    // 除法
    divid() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    // 暫存數字
    setPrevious() {
      // 暫存值 ( 按下運算符號時要清空目前的 current )
      this.previous = this.current;
      // 表示使用者確實按下任何一個運算子
      this.operatorClicked = true;
    },
    // 等於
    equal() {
      if(this.operator) {
        this.current = `${this.operator(
          parseFloat(this.previous),
          parseFloat(this.current)
        )}`;
        this.operator = null;
        this.operatorClicked = false;
      }
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
