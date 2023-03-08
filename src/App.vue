<template>
  <div class="main">
    <div class="main-container">
      <div class="holder">
        <div class="numbers">
          <button
            class="btn-number"
            v-for="n in 10"
            :key="n"
            @click="append(n)"
          >
            <span>{{ n - 1 }}</span>
            <!-- n-1 to display 0 -->
          </button>
        </div>
        <div class="screen" v-show="!warning">{{ res || 0 }}</div>
        <div class="warning" v-show="warning">
          Operation not available! , Division by zero is not allowed
        </div>
      </div>

      <div class="opearation">
        <button @click="opearatorHandler('+')" class="btn-add">
          <span>+</span>
        </button>
        <button @click="opearatorHandler('-')" class="btn-subtract">
          <span>-</span>
        </button>
        <button @click="opearatorHandler('*')" class="btn-multiplay">
          <span>X</span>
        </button>
        <button @click="opearatorHandler('/')" class="btn-divide">
          <span>/</span>
        </button>
        <button @click="calkHandler" class="btn-equal"><span>=</span></button>
        <button @click="clearHandler" class="btn-equal"><span>C</span></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  data() {
    return {
      firstNum: "",
      secondNum: "",
      opearator: "",
      res: "",
      warning: false,
    };
  },
  methods: {
    opearatorHandler: function (opearator) {
      if (this.firstNum === "") {
        this.calkHandler();
      } else if (this.opearator !== "") {
        return;
      } else {
        this.opearator = opearator;
        this.res = this.firstNum + this.opearator + this.secondNum;
      }
    },
    clearHandler: function () {
      //Reaset All data
      (this.firstNum = ""),
        (this.secondNum = ""),
        (this.opearator = ""),
        (this.res = "");
      this.warning = false;
    },
    calkHandler: function () {
      if (this.opearator != "" && this.firstNum === "") {
        this.clearHandler();
      } else if (this.opearator === "/" && this.secondNum === 0) {
        this.warning = true;
      } else {
        this.res = parseFloat(
          eval(this.firstNum + this.opearator + this.secondNum).toFixed(4)
        );
        this.firstNum = "";
        this.secondNum = "";
      }
    },
    append: function (n) {
      if (this.firstNum === "" && this.opearator === "") {
        this.firstNum = n - 1;
        this.res = this.firstNum; // display first number
      } else if (this.firstNum !== "" && this.opearator === "") {
        this.firstNum = +(`${this.firstNum}` + `${n - 1}`); // Make the first number more than one digit
        this.res = this.firstNum;
      } else if (this.secondNum == "") {
        this.secondNum = n - 1;
        this.res = this.firstNum + this.opearator + this.secondNum;
      } else {
        this.secondNum = +(`${this.secondNum}` + `${n - 1}`); // Make the second number more than one digit
        this.res = this.firstNum + this.opearator + this.secondNum;
      }
    },
  },
};
</script>

<style>
.main-container {
  width: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
  height: 400px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border: 2px solid #000;
  border-radius: 20px;
  padding: 7px;
  background-color: #0000000d;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
}

.numbers {
  flex: 70%;
  padding: 10px;
  height: 60%;
}
.screen {
  display: flex;
  align-items: center;
  justify-content: center;
  flex: 70%;
  height: 20%;
  padding: 10px;
  font-size: 45px;
  border-radius: 5px;
  background-color: #00000025;
  margin: auto;
  width: 300px;
}
.warning {
  display: flex;
  align-items: center;
  justify-content: center;
  flex: 70%;
  height: 20%;
  padding: 10px;
  border-radius: 5px;
  background-color: #fff3cd;
  border: 1px solid #997404;
  color: #997404;
  margin: auto;
  width: 100%;
}
.warning p {
  font-size: 45px;
}
.btn-number {
  flex: 50%;
  width: 100px;
  height: 100px;
  margin-right: 5px;
  margin-bottom: 10px;
  background-color: #b1acac;
  color: #fff;
  border: 1px solid #333;
  cursor: pointer;
}
.btn-number span {
  font-size: 25px;
}
.opearation {
  flex: 40%;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}
.opearation button {
  width: 50px;
  height: 50px;
  font-weight: bold;
  margin-bottom: 5px;
  border-radius: 50%;
  background-color: orange;
  border: 1px solid #ccc;
  color: #fff;
  cursor: pointer;
}
.opearation button:hover {
  transform: scale(1.1);
  transition: 0.5s;
}
</style>
