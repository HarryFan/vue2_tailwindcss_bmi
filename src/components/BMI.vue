<template>
  <div class="container h-screen flex items-center justify-center">
    <div class="inner rounded-lg bg-teal-500 p-6 relative" style="width: 350px;">
     
     <div class="B-wrap">
      <span class="text-white font-bold absolute right-0 top-0 mr-4 mt-2">B</span>
     <div class="content-padding"></div> 
    </div>
      <div id="BMI">
        <form @submit.prevent="calculateBMI" class="mt-4">
          <div class="form-group">
            <label for="height" class="block text-white font-medium mb-2">身高 (cm):</label>
            <input type="text" id="height" v-model="height" required class="form-input w-full">
          </div>
          <div class="form-group">
            <label for="weight" class="block text-white font-medium mb-2">體重 (kg):</label>
            <input type="text" id="weight" v-model="weight" required class="form-input w-full">
          </div>
          <div class="form-group mt-1">
            <button type="submit"
              class="bg-teal-600 text-white font-medium py-1 px-4 rounded-full hover:bg-teal-700 border border-white">計算</button>
          </div>
        </form>
        <p v-if="bmi" class="mt-4 text-white font-medium">您的BMI是: {{ bmi }}</p>
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
        bmi: ''
      }
    },
    methods: {
      calculateBMI() {
        let bmi = this.weight / (this.height / 100 * this.height / 100)
        this.bmi = bmi.toFixed(2)
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
  }

  .inner:hover {
    clip-path: circle(75%);
    background: #00B6FF;
  }

  .inner span {
    color: white;
    font-weight: bold;
    transition: color .5s;
    position: absolute;
    top: 27px;
    right: 14px;
    z-index: 2; /* 新增的屬性 */
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

  .B-wrap >span{}
  .content-padding{
    height:20px;
  }
</style>