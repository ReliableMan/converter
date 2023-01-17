<template>
  <div class="mt-5 xl:mt-9 ml-[15px] min-[1600px]:mt-[30px ] mb-5">
    <h3 class="font-bold text-[20px] md:text-[26px] min-[1600px]:text-[36px] leading-[140%] text-[#0F4471] mb-5 md:ml-[20px] xl:ml-[45px] min-[1600px]:ml-[65px]">Курс рубля</h3>
    
    <div class="md:flex md:flex-wrap xl:ml-[10px]">
    <div v-for="(current, index) in currency" :key="current.id" 
    class="w-[330px] md:w-[344px] xl:w-[370px] min-[1600px]:w-[460px] h-[242px] md:h-[312px] min-[1600px]:h-[330px] bg-[#f8f8f8] rounded-2xl mb-5 md:ml-5 xl:ml-[30px] hover:drop-shadow-md cursor-pointer">
    
      <div class="pt-[25px] md:pt-[38px] ml-6 min-[1600px]:ml-[30px]">
        <!-- при четном индексе красная картинка -->
        <img class="w-[49px] md:w-[51px] xl:w-[55px] min-[1600px]:w-[70px] h-[50px] md:h-[52px] xl:h-[56px] min-[1600px]:h-[70px]" v-if="index % 2" src="../assets/svg/red-money.svg" alt="red-money-img"/>
        <!-- при нечетном индексе синия картинка -->
        <img class="w-[49px] md:w-[51px] xl:w-[55px] min-[1600px]:w-[70px] h-[50px] md:h-[52px] xl:h-[56px] min-[1600px]:h-[70px]" v-else src="../assets/svg/blue-money.svg" alt="blue-money-img"/>
        <!-- CharCode валюты -->
        <p class="mt-4 md:mt-[30px] font-bold text-[17px] md:text-[18px] xl:text-[20px]  leading-[140%] text-[#0F4471]">{{ current.CharCode }}</p>
        <!-- название валюты -->
        <p class="mt-2 md:mt-[20px] font-normal text-[14px] xl:text-[15px] min-[1600px]:text-[16px] leading-[140%] text-[#111111] ">{{ current.Name }}</p>
        <!-- номинал -->
        <div class="flex mt-5 md:mt-[30px]">
         <img class="w-[8px] min-[1600px]:w-[10px]" src="../assets/svg/Ellipse 53.svg" alt="red-round"/>
         <p class="ml-2 text-sm xl:text-[15px] min-[1600px]:text-[16px] xl:leading-5 min-[1600px]:leading-[140%] font-medium text-[#1C1C1C]">Номинал: {{ current.Nominal }}</p>
        </div>
        <!-- курс -->
        <div class="flex mt-2 md:mt-[15px]">
         <img class="w-[8px] min-[1600px]:w-[10px]" src="../assets/svg/Ellipse 53.svg" alt="red-round"/>
         <p class="ml-2 text-sm xl:text-[15px] min-[1600px]:text-[16px] font-medium text-[#1C1C1C] ">Курс: {{ current.Value }}</p>
        </div>
      </div>
    </div>
  </div>
      <!-- Футер -->
    <div class="w-[330px] md:w-[708px] xl:w-[1164px] min-[1100px]:w-[1075px] min-[1600px]:w-[1439px] h-[166px] md:h-[101px] xl:h-[127px] mb-[98px] bg-[#F8F8F8] rounded-2xl md:ml-[20px] xl:ml-[40px]">
      <div class="pt-8 xl:pt-[2.5rem] ml-7 md:flex md:ml-[25px] min-[1600px]:ml-[31px]">
        <img class="w-[42px] md:w-[39px] xl:w-[44px] min-[1600px]:w-[50px] h-[42px] md:h-[40px] xl:h-[45px] min-[1600px]:h-[48px]" src="../assets/svg/blue-info.svg" alt="blue-info"/>
        <div class="pt-[20px] md:pt-3 md:pl-[25px] xl:pl-[19px] min-[1600px]:pl-[30px] text-[16px] md:text-[18px] xl:text-[20px] font-bold leading-[140%] text-[#0F4471] md:flex md:space-x-1">
          <p>Телефон: <a href="tel:8 800 888-90-28">8 (800) 888-90-28,</a></p>
          <p>email: <a href="mailto:info@example.ru">info@example.ru.</a></p>
        </div>
      </div>
    </div>
    <!-- Div за которым следит observer и динамически подгружает список (как бесконечная лента) -->
    <div class="md:h-[10vh] min-[1000px]:h-[20vh] xl:h-[40vh] " ref="observer"></div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'SecondPage',
  data () {
    return {
      currency: [],
      end: 0,
    }
  },
  methods: {
    async fetchCurrency () {
      try {
        this.end += 3;
        const response = await axios.get('https://www.cbr-xml-daily.ru/daily_json.js');
        const result = Object.values(response.data.Valute);
        this.currency = result.slice(0, this.end);
      } catch (error) {
        console.error
      }
    }
  },
  mounted () {
    const options = {
      rootMargin: '0px',
      threshold: 1.0
    };
    const callback = (entries, observer) => {
      entries[0].isIntersecting ? this.fetchCurrency() : ''
    };
    const observer = new IntersectionObserver(callback, options);
    observer.observe(this.$refs.observer)
  },
}
</script>


