<template>
  <div id="calculator">
    <div class="display">{{ cur }}</div>
    <div class="keyPad">
      <button @click="allClear" class="clear">AC</button>
      <button @click="sign" class="sign">+/-</button>
      <button @click="percent" class="percent">%</button> 
      <button @click="divide" :class="[operatorActive === 'divide' ? 'lighten' : '', 'operator']">/</button>
      <button @click="appendVal('7')" class="number">7</button>
      <button @click="appendVal('8')" class="number">8</button>
      <button @click="appendVal('9')" class="number">9</button>
      <button @click="multiply" :class="[operatorActive === 'multiply' ? 'lighten' : '', 'operator']">x</button>
      <button @click="appendVal('4')" class="number">4</button>
      <button @click="appendVal('5')" class="number">5</button>
      <button @click="appendVal('6')" class="number">6</button>
      <button @click="subtract" :class="[operatorActive === 'subtract' ? 'lighten' : '', 'operator']">-</button>
      <button @click="appendVal('1')" class="number">1</button>
      <button @click="appendVal('2')" class="number">2</button>
      <button @click="appendVal('3')" class="number">3</button>
      <button @click="add" :class="[operatorActive === 'add' ? 'lighten' : '', 'operator']">+</button>
      <button @click="decimal" class="decimal">.</button>
      <button @click="appendVal('0')" class="number">0</button>
      <button @click="equal" class="equals">=</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      cur: '0',
      prev: '',
      toggleCur: false,
      operator: null,
      operatorActive: null
    }
  },
  methods: {
    allClear() {
      this.cur = '0'
      this.prev = ''
      this.toggleCur = false
      this.operator = null
      this.operatorActive = null
    },
    appendVal(num) {
      if(!this.toggleCur) {
        this.cur = this.cur.concat(num)
      } else {
        this.cur = num
        this.toggleCur = false
      }
    },
    sign() {
      if(this.cur) {
        this.cur = this.cur.charAt(0) === '-' ?
          this.cur.slice(1) : `-${this.cur}`
      }
    },
    percent() {
      if(this.cur) {
        this.cur = `${parseFloat(this.cur)/100}`
      }
    },
    decimal() {
      if(this.cur.indexOf('.') === -1) {
        this.appendVal('.')
      }
    },
    divide() {
      if(!this.prev) {
        this.prev = this.cur
      }else if(!this.toggleCur) {
        this.prev = `${parseFloat(this.prev)/parseFloat(this.cur)}`
        this.cur = this.prev
      }
      this.toggleCur = true
      this.operatorActive = 'divide'
      this.operator = (prev, cur) => prev/cur
    },
    multiply() {
      if(!this.prev) {
        this.prev = this.cur
      }else if(!this.toggleCur) {
        this.prev = `${parseFloat(this.prev)*parseFloat(this.cur)}`
        this.cur = this.prev
      }
      this.toggleCur = true
      this.operatorActive = 'multiply'
      this.operator = (prev, cur) => prev*cur
    },
    subtract() {
      if(!this.prev) {
        this.prev = this.cur
      }else if(!this.toggleCur) {
        this.prev = `${this.operator(parseFloat(this.prev),parseFloat(this.cur))}`
        this.cur = this.prev
      }
      this.toggleCur = true
      this.operatorActive = 'subtract'
      this.operator = (prev, cur) => prev-cur
    },
    add() {
      if(!this.prev) {
        this.prev = this.cur
      }else if(!this.toggleCur) {
        this.prev = `${this.operator(parseFloat(this.prev),parseFloat(this.cur))}`
        this.cur = this.prev
      }
      this.toggleCur = true
      this.operatorActive = 'add'
      this.operator = (prev, cur) => prev+cur
    },
    equal() {
      if(!this.toggleCur) {
        this.cur = `${this.operator(parseFloat(this.prev),parseFloat(this.cur))}`
        this.prev = ''
        this.toggleCur = true
        this.operator = null
        this.operatorActive = null
      }
      console.log(this.operatorActive)
    }
  }
}
</script>


<style scoped>

  #calculator {
    max-width: 400px;
    margin: auto;
    border: solid white 2px;
    border-radius: 12px;
  }

  .display {
    height: 75px;
    padding: 10px 5px 0 5px;
    border: solid white 1px;
    border-radius: 10px 10px 0 0;
    background-color: rgb(40, 40, 40);
    color: white;
    font-size: 48px;
    text-align: right;
    overflow: hidden;
  }

  .keyPad {
    display: flex;
    flex-wrap: wrap;
  }

  button {
    flex: 1 0 25%;
    height: 80px;
    color: white;
    font-size: 36px;
  }

  .number {
    background-color: rgb(0, 106, 133);
  }

  .operator {
    background-color: rgb(187, 123, 5);
  }

  .lighten {
      background-color: rgb(228, 166, 51);
    }

  .equals {
    flex: 1 0 50%;
    background-color: rgb(56, 128, 8);
    border-radius: 0 0 10px 0;
  }

  .decimal {
    background-color: rgb(82, 23, 94);
    border-radius: 0 0 0 10px;
  }

  .sign, .percent {
    background-color: rgb(100, 85, 57);
  }

  .clear {
    background-color: rgb(134, 0, 22);
  }
</style>
