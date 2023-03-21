<template>
  <div class="bg-gray-100 min-h-screen flex flex-col items-center justify-center">
    <div class="w-96 bg-white shadow-lg rounded-lg p-6 card">
      <h1 class="text-2xl font-semibold mb-6">BMI 指數計算器</h1>
      <div class="mb-4">
        <label for="height" class="block text-sm mb-1">身高 (公分)</label>
        <input type="number" v-model="height" id="height" placeholder="輸入您的身高"
          class="w-full p-2 border border-gray-300 rounded">
      </div>
      <div class="mb-6">
        <label for="weight" class="block text-sm mb-1">體重 (公斤)</label>
        <input type="number" v-model="weight" id="weight" placeholder="輸入您的體重"
          class="w-full p-2 border border-gray-300 rounded">
      </div>
      <button @click="calculateBMI" class="w-full bg-blue-500 text-white py-2 rounded">計算 BMI</button>
      <div v-if="bmi" class="mt-6 text-center">
        <p class="text-lg">您的 BMI 指數為: <span class="font-semibold">{{ bmi.toFixed(1) }}</span></p>
        <p class="text-lg">分類: <span class="font-semibold">{{ bmiCategory }}</span></p>
      </div>
      <transition name="fade">
        <div v-if="showAnimation" class="fixed top-0 left-0 w-full h-full bg-blue-500 opacity-50"></div>
      </transition>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        height: "",
        weight: "",
        bmi: null,
        showAnimation: false
      };
    },
    computed: {
      // eslint-disable-next-line vue/return-in-computed-property
      bmiCategory() {
        if (this.bmi < 18.5) return "過輕";
        if (this.bmi >= 18.5 && this.bmi < 24.9) return "正常";
        if (this.bmi >= 24.9 && this.bmi < 29.9) return "過重";
        if (this.bmi >= 29.9) return "肥胖";
      }
    },
    methods: {
      calculateBMI() {
        if (this.height && this.weight) {
          this.bmi = (this.weight / ((this.height / 100) * (this.height / 100)));
          this.showAnimation = true;
          setTimeout(() => {
            this.showAnimation = false;
          }, 1000);
        }
      }
    }
  };
</script>

<style scoped>
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
    transform: scale(0.95);
    /* 改變尺寸 */
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s, transform 0.5s;
    /* 添加 transform 過渡動畫 */
  }

  .card {
    clip-path: polygon(100% 0, 100% 100%, 0 100%);
    /* 右上角到左下角 */
    transition: clip-path 0.5s;
    /* 過渡動畫效果 */
  }

  .card:hover {
    background-color: rgba(229, 231, 235, 1);
    /* 背景顏色淺灰色 */
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    /* 陰影效果 */
    clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
    /* 顯示完整卡片 */
  }
</style>