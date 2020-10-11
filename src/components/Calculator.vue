<template>
  <div class="torso">
    <div class="d-flex align-items-center min-vh-100">
      <div class="container">
        <!-- View -->
        <div class="card">
          <div class="card-header">
            <div class="text-center">
              <h4>{{ display || "Press Some Number 🔢" }}</h4>
            </div>
          </div>
          <div class="card-body">
            <div class="row"></div>
            <div class="row">
              <div @click="clear" class="col btn btn-magenta">C</div>
              <div @click="sign" class="col btn btn-magenta">+/-</div>
              <div @click="percent" class="col btn btn-magenta">%</div>
              <div @click="divide" class="col btn btn-magenta">/</div>
            </div>
            <div class="row">
              <div @click="append('7')" class="col btn btn-teal">7</div>
              <div @click="append('8')" class="col btn btn-teal">8</div>
              <div @click="append('9')" class="col btn btn-teal">9</div>
              <div @click="multiply" class="col btn btn-magenta">*</div>
            </div>
            <div class="row">
              <div @click="append('4')" class="col btn btn-teal">4</div>
              <div @click="append('5')" class="col btn btn-teal">5</div>
              <div @click="append('6')" class="col btn btn-teal">6</div>
              <div @click="minus" class="col btn btn-magenta">-</div>
            </div>
            <div class="row">
              <div @click="append('1')" class="col btn btn-teal">1</div>
              <div @click="append('2')" class="col btn btn-teal">2</div>
              <div @click="append('3')" class="col btn btn-teal">3</div>
              <div @click="add" class="col btn btn-magenta">+</div>
            </div>
            <div class="row">
              <div @click="append('0')" class="col-6 btn btn-teal">0</div>
              <div @click="fullstop" class="col btn btn-teal">.</div>
              <div @click="equal" class="col btn btn-magenta">=</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      display: "",
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.display = "";
    },
    sign() {
      this.display =
        this.display.charAt(0) === "-"
          ? this.display.slice(1)
          : `-${this.display}`;
    },
    percent() {
      this.display = `${parseFloat(this.display) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.display = "";
        this.operatorClicked = false;
      }
      this.display = `${this.display}${number}`;
    },
    fullstop() {
      if (this.display.indexOf(".") === -1) {
        this.display = `${this.display}.`;
      }
    },
    setPrevious() {
      this.previous = this.display;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.display = `${this.operator(
        parseFloat(this.display),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
  },
};
</script>

<style scoped>
.torso {
  background-color: #fed8b1;
}
.btn {
  border-radius: 0px;
}
.btn-teal {
  color: #000;
  font-weight: bolder;
}
.btn-teal:hover {
  background-color: #47ffb3;
  color: #fff;
}
.btn-magenta {
  color: #ff4793;
  font-weight: bolder;
}
.btn-magenta:hover {
  background-color: #ff4793;
  color: #fff;
}
</style>
