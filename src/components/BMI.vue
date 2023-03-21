<template>
  <div class="container h-screen flex items-center justify-center">
    <div class="inner rounded-lg bg-teal-500  relative" style="width: 350px;">
      <div class="B-container">
        <span class="">B</span>
      </div>
      <div class="content pt-8">
        <div id="BMI">
          <form @submit.prevent="calculateBMI" class="mt-4">
            <div class="form-group">
              <label for="height" class="block text-white font-medium mb-2">身高 (cm):</label>
              <input type="text" id="height" v-model="height" required class="form-input w-full p-1">
            </div>
            <div class="form-group">
              <label for="weight" class="block text-white font-medium mb-2 mt-2">體重 (kg):</label>
              <input type="text" id="weight" v-model="weight" required class="form-input w-full p-1">
            </div>
            <div class="form-group mt-1">
              <button type="submit"
                class="bg-teal-600 text-white font-medium py-1 px-4 rounded-full hover:bg-teal-700 border border-white mt-2">計算</button>
            </div>
          </form>
          <p v-if="bmi" class="mt-4 text-white font-medium">您的BMI是: {{ bmi }},{{ bmiStatus }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        weight: '',
        height: '',
        bmi: '',
        bmiStatus: ''
      }
    },
    methods: {
      calculateBMI() {
        let bmi = this.weight / (this.height / 100 * this.height / 100)
        this.bmi = bmi.toFixed(2);
        if (bmi < 18.5) {
          this.bmiStatus = "體重過輕";
        } else if (bmi >= 18.5 && bmi < 24) {
          this.bmiStatus = "正常範圍";
        } else if (bmi >= 24 && bmi < 27) {
          this.bmiStatus = "過重";
        } else if (bmi >= 27 && bmi < 30) {
          this.bmiStatus = "輕度肥胖";
        } else if (bmi >= 30 && bmi < 35) {
          this.bmiStatus = "中度肥胖";
        } else {
          this.bmiStatus = "重度肥胖";
        }
      }
    }
  }
</script>
<style>
  .container {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .inner {
    background: rgb(7, 218, 165);
    padding: 1em;
    border-radius: 10px;
    width: 250px;
    clip-path: circle(10% at 90% 20%);
    transition: all .5s ease-in-out;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    /* 新增的屬性 */

  }

  .inner:hover {
    clip-path: circle(75%);
    background: #00B6FF;
    overflow: hidden;
  }


  .B-container {
    position: absolute;
    top: 20%;
    left: 90%;
    transform: translate(-50%, -50%);
    z-index: 2;
  }

  .inner span {
    color: white;
    font-weight: bold;
    transition: color .5s;
    display: inline-block;
  }

  .inner:hover span {
    color: rgba(255, 255, 255, 0);
  }

  .inner:hover span {
    color: rgba(255, 255, 255, 0);
  }

  .inner h1 {
    color: white;
    margin: 0;
  }


  .inner p {
    color: white;
    font-size: .8rem;
  }

  .B-wrap {
    display: flex;
    position: relative;
    height: 63px;
    justify-content: end;
  }

  .B-wrap>span {

    color: white;
    font-weight: bold;
    transition: color .5s;

    left: 21px;
    top: 18px;
    width: 63px;

    display: block;
    height: 63px;

    position: relative;
  }

  .content-padding {
    height: 63px;
  }
</style>