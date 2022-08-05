<template>
  <h1>calculator</h1>
  <div class="calculator">
    <div class="dispaly">{{ current || 0 }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="percentage" class="btn">%</div>
    <div @click="divide" class="btn">/</div>
    <div @click="multiply" class="btn">*</div>
    <div @click="minus" class="btn">-</div>
    <div @click="numberclick('7')" class="btn">7</div>
    <div @click="numberclick('8')" class="btn">8</div>
    <div @click="numberclick('9')" class="btn">9</div>
    <div @click="add" class="btn">+</div>
    <div @click="numberclick('4')" class="btn">4</div>
    <div @click="numberclick('5')" class="btn">5</div>
    <div @click="numberclick('6')" class="btn">6</div>
    <div @click="numberclick('1')" class="btn">1</div>
    <div @click="numberclick('2')" class="btn">2</div>
    <div @click="numberclick('3')" class="btn">3</div>
    <div @click="numberclick('0')" class="btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn">=</div>
  </div>
</template>

<script>

export default {
  name: "CalCulator",
  data() {
    return {
      current: "",
      previous: null,
      operators: null,
      operatorclick:false,
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    percentage() {
      this.current = parseFloat(this.current / 100);
    },
    numberclick(number) {
      if(this.operatorclick)
      this.current='';
      
      this.operatorclick=false;
      this.current = this.current + number;
    },
    dot() {
      if (this.current.indexOf(".") === -1) this.numberclick(".");
    },
    divide() {
      this.operators = (a, b) => a / b;
      this.previous = this.current;
      this.operatorclick = true;
    },
    multiply() {
      this.operators = (a, b) => a * b;
       this.previous = this.current;
      this.operatorclick = true;
    },
    minus() {
      this.operators = (a, b) => parseFloat(a - b);
      this.previous = this.current;
      this.operatorclick = true;
    },
    add() {
      this.operators = (a, b) => parseFloat(a + b);
       this.previous = this.current;
      this.operatorclick = true;
    },
    equal() {
      this.current = `${this.operators(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous=null
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 12%;
  height: 300px;
  margin: auto;
}
.dispaly {
  color: blue;
  display: inline-flex;
  text-align: center;
  justify-content: center;
  padding-top: 10px;
  width: 100%;
  height: 50px;
  margin: 10px auto;
  border: 2px solid rgb(19, 31, 199);
}
.btn {
  border: 2px solid rgb(29, 218, 218);
  width: 50px;
  height: 40px;
  text-align: center;
  padding: 10px 0 0 0;
  justify-content: center;
  cursor: pointer;
}
.btn:hover {
  background: gray;
}
</style>
