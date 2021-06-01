<template>
    <div class="container col-4">

      <div class="row">
        <div class="col border border-dark text-center bg-secondary text-white">
          {{currentValue || 0}}
        </div>
      </div>

      <div class="row">
        <div @click="clearView " class="col border border-dark bg-$gray-200 text-center">
          C
        </div>
        <div @click="negateNumber" class="col border border-dark bg-$gray-200 text-center">
          +/-
        </div>
        <div @click="percentage" class="col border border-dark bg-$gray-200 text-center">
          %
        </div>
        <div @click="operationMethod('/')" class="col border border-dark bg-warning text-center">
          /
        </div>
      </div>

      <div class="row">
        <div @click="appendNumber(7)" class="col border border-dark bg-$gray-200 text-center">
          7
        </div>
        <div @click="appendNumber(8)" class="col border border-dark bg-$gray-200 text-center">
          8
        </div>
        <div @click="appendNumber(9)" class="col border border-dark bg-$gray-200bg-$gray-200 text-center">
          9
        </div>
        <div @click="operationMethod('X')" class="col border border-dark bg-warning text-center">
          X
        </div>
      </div>

      <div class="row">
        <div @click="appendNumber(4)" class="col border border-dark bg-$gray-200bg-$gray-200 text-center">
          4
        </div>
        <div @click="appendNumber(5)" class="col border border-dark bg-$gray-200 text-center">
          5
        </div>
        <div @click="appendNumber(6)" class="col border border-dark bg-$gray-200 text-center">
          6
        </div>
        <div @click="operationMethod('-')" class="col border border-dark bg-warning text-center">
          -
        </div>
      </div>

      <div class="row">
        <div @click="appendNumber(1)" class="col border border-dark bg-$gray-200 text-center">
          1
        </div>
        <div @click="appendNumber(2)" class="col border border-dark bg-$gray-200y text-center">
          2
        </div>
        <div @click="appendNumber(3)" class="col border border-dark bg-$gray-200 text-center">
          3
        </div>
        <div @click="operationMethod('+')" class="col border border-dark bg-warning text-center">
          +
        </div>
      </div>

      <div class="row">
        <div @click="appendNumber(0)" class="col-6 border border-dark bg-$gray-200 text-center">
          0
        </div>
        <div @click="decimalNumber" class="col-3 border border-dark bg-$gray-200 text-center">
          .
        </div>
        <div @click="calculateMethod" class="col-3 border border-dark bg-warning text-center">
          =
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      currentOperation: null, 
      previousValue: '', 
      currentValue: '',
      selectedOperation: ''
    }
  }, 
  methods: {
    operationMethod(operation) {
      if(this.currentValue === '' || this.currentValue === '0') {
        this.currentValue = 0 
      }
      this.selectedOperation = operation 
      this.previousValue = this.currentValue
      this.currentValue = ''
    },
    calculateMethod() {
      switch(this.selectedOperation) {
        case '+':
          this.currentValue = parseFloat(this.currentValue) + parseFloat(this.previousValue)
          break;
        case '-':
          this.currentValue = parseFloat(this.previousValue) - parseFloat(this.currentValue)
          break;
        case 'X':
          this.currentValue = parseFloat(this.previousValue) * parseFloat(this.currentValue)
          break;
        case '/':
          this.currentValue = parseFloat(this.previousValue) / parseFloat(this.currentValue)
          break;
      }
    },
    appendNumber(number) {
      if(this.currentValue === '0' || this.currentValue === 0) {
        this.currentValue = `${number}`
      }
      else { 
        this.currentValue = `${this.currentValue}${number}`
      }
      
    }, 
    percentage() {
      if(this.currentValue === '0' || this.currentValue === '') {
        alert('Can not apply "%" operation to the value of 0!')
      } 
      else {
        this.currentValue =  `${parseFloat(this.currentValue) / 100}`  
      }    
    }, 
    negateNumber() {
      this.currentValue = this.currentValue[0] === '-' ? `${-1 * parseFloat(this.currentValue)}` : `-${this.currentValue}`
    }, 
    clearView() {
      this.currentValue = ''
    },
    decimalNumber() {
      if(this.currentValue === '0' || this.currentValue === 0) {
        this.currentValue = `${this.currentValue}.`
      }
      if(this.currentValue[1] !== '.'){
        this.currentValue = `0.${this.currentValue}`
      }
    }
  }
}
</script>

