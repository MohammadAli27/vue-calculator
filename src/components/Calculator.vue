<template>
  <div class="calculator">
    <div id="1" style="border-radius: 10px 10px 0 0;" class="display">
      {{ current || 0 }}
    </div>
    <div @click="clear" class="oprator">C</div>
    <div @click="sign" class="oprator">+/-</div>
    <div @click="percent" class="oprator">%</div>
    <div @click="dvide" class="oprator">÷</div>
    <div @click="append(7)">7</div>
    <div @click="append(8)">8</div>
    <div @click="append(9)">9</div>
    <div @click="times" class="oprator">&times;</div>
    <div @click="append(4)">4</div>
    <div @click="append(5)">5</div>
    <div @click="append(6)">6</div>
    <div @click="minus" class="oprator">-</div>
    <div @click="append(1)">1</div>
    <div @click="append(2)">2</div>
    <div @click="append(3)">3</div>
    <div @click="add" class="oprator">+</div>
    <div
      style="border-radius: 0 0 0 10px;"
      @click="append"
      class="two-col zero"
    >
      0
    </div>
    <div @click="dot">.</div>
    <div style="border-radius: 0 0 10px 0;" @click="equal" class="oprator">
      =
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      oClicked: false,
    };
  },
  methods: {
    setPrevius() {
      this.pre = this.current;
      this.oClicked = true;
    },
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = parseFloat(this.current / 100);
    },
    append(num) {
      if (this.oClicked) {
        this.current = "";
        this.oClicked = false;
      }
      this.current = `${this.current}${num}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) this.append(".");
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevius();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevius();
    },
    dvide() {
      this.operator = (a, b) => a / b;
      this.setPrevius();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevius();
    },
    equal() {
    this.pre = null;
      if (this.pre != this.current) {
        this.current = `${this.operator(
          parseFloat(this.current),
          parseFloat(this.pre)
        )}`;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style>
body {
  background-color: #222;
}
.calculator {
  display: grid;
  box-shadow: 0 0 10px black;
  border-radius: 8px;
  width: 25vw;
  margin: auto;
  font-size: 24px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minimax(50px, auto);
}

.calculator > div {
  border: 1px solid #222;
  background-color: #eee;
  padding: 10px;
  user-select: none;
  cursor: pointer;
  transition: 200ms all;
}
.calculator > div:not(.display):hover {
  filter: brightness(85%);
  transition: 200ms all;
}
.oprator {
  background-color: #ff9100 !important;
  color: #fff;
}

.display {
  grid-column: 1/5;
  background-color: #333333 !important;
  color: #fff;
}
.radius {
  border-radius: 10px;
  overflow: hidden;
}
.two-col {
  grid-column: 1/3;
}

.zero {
  text-align: left;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
