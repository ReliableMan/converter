<template>
  <div>
    <div class="mt-5 xl:mt-9 min-[1600px]:mt-[30px] ml-[15px] mb-5 md:ml-[30px] xl:ml-[55px] min-[1600px]:ml-[80px]">
      <h3 class="text-xl md:text-[26px] min-[1600px]:text-[34px] md:leading-[30px] min-[1600px]:leading-[40px] font-bold md:font-medium text-[#0F4471]">Валютный калькулятор</h3>
        <div class="flex flex-col md:flex-row">
          <!-- 1 потомок -->
          <div>
            <!-- Валюта 1 -->
            <div class="flex flex-col mt-6">
              <label class="mb-[14px] text-[14px] min-[1600px]:text-[16px] leading-4 min-[1600px]:leading-[19px] text-[#2C3A4B]" for="currency1">Валюта 1</label>
              <input v-model.lazy="currency1" list="allCurrency"
              class="w-[330px] md:w-[337px] xl:w-[561px] min-[1600px]:w-[699px] h-[46px] xl:h-[50px] pl-5 border border-slate-300 placeholder:text-[12px] min-[1600px]:placeholder:text-[14px] placeholder:leading-[28px] rounded-[5px] focus:outline-none focus:ring-1 focus:ring-sky-500 focus:border-[#EEF5FF]" type="text" id="currency1" placeholder="Введите название или код">
              <datalist id="allCurrency">
                <option v-for="current in currency" :key="current.id" :value="current.Name"></option>
              </datalist>
            </div>
            <!-- Валюта 2 -->
            <div class="flex flex-col mt-6">
              <label class="mb-[14px] text-[14px] leading-4 text-[#2C3A4B]" for="currency2">Валюта 2</label>
              <input v-model.lazy="currency2" list="allCurrency"
              class="w-[330px] md:w-[337px] xl:w-[561px] min-[1600px]:w-[699px] h-[46px] xl:h-[50px] pl-5 border border-slate-300 placeholder:text-[12px] min-[1600px]:placeholder:text-[14px] placeholder:leading-[28px] rounded-[5px] focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500" type="text" id="currency2" placeholder="Введите название или код">
              <datalist id="allCurrency">
                <option v-for="current in currency" :key="current.id " :value="current.Name"></option>
              </datalist>
            </div>
            <!-- Количество -->
            <div class="flex flex-col mt-6">
              <label class="mb-[14px] text-[14px] leading-4 text-[#2C3A4B]" for="amount">Количество</label>
              <input v-model.number="amount"
              class="w-[330px] md:w-[337px] xl:w-[561px] min-[1600px]:w-[699px] h-[46px] xl:h-[50px] pl-5 border border-slate-300 placeholder:text-[12px] min-[1600px]:placeholder:text-[14px] placeholder:leading-[28px] rounded-[5px] focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500" type="number" id="amount" placeholder="Введите число">
            </div>
            <!-- Итого -->
            <div class="w-[330px] md:w-[336px] xl:w-[561px] min-[1600px]:w-[699px] h-[82px] md:h-[108px] min-[1600px]:h-[127px] mt-[19px] rounded-2xl bg-[#EEF5FF] flex items-center">
              <img class="ml-[26px] w-[42px] md:w-[40px] xl:w-[45px] min-[1600px]:w-[50px]" src="../assets/svg/red-info.svg" alt="info-blue-img"/>
              <p class="ml-[19px] text-[14px] md:text-[16px] xl:text-[20px] min-[1600px]:text-[24px] leading-[140%] font-bold text-[#0F4471]">Итого: {{ result ? result : '...' }} </p>
            </div>
          </div>
          <!-- 2 потомок -->
          <div class="md:ml-7 xl:ml-10">
            <info/>
          </div>
        </div>
    </div>
    <myFooter/>
  </div>
</template>

<script>
import info from '../components/SectionInfo/info.vue';
import myFooter from '../components/Footer/footer.vue';
import axios from 'axios';
export default {
  name: 'IndexPage',
  components: {
    info, myFooter
  },
  data () {
    return {
      curr: [],
      currency: [],
      currency1: null,
      currency2: null,
      amount: null,
      result: null,
    }
  }, 
  methods: {
    async fetchCurrency () {
      try {
        // получаем весь список валют
        const response = await axios.get('https://www.cbr-xml-daily.ru/daily_json.js');
        this.currency = Object.values(response.data.Valute);
        // получаем список валют приравненных к рублю
        const response2 = await axios.get('https://www.cbr-xml-daily.ru/latest.js');
        this.curr = response2.data.rates;
      } catch (error) {
        console.error
      }
    },
   async getCurrency () {
    // получаем код валюты из 1 и 2 инпута
     let name1 = await this.currency.find(el => el.Name === this.currency1).CharCode;
     let name2 = await this.currency.find(el => el.Name === this.currency2).CharCode;
    //  находим конкретную валюту в списке 
     let element1 = this.curr[name1];
     let element2 = this.curr[name2];
    //  если валюты равны друг другу, вписываем данные из поля amount
      if(this.currency1 === this.currency2) {
        this.result = this.amount
      } 
      /* если не равны находим соотношение одной к другой, 
      умножаем на количество и обрезаем до 2 знаков после точки */
      this.result = ((element2 / element1) * this.amount).toFixed(2);
    }
  },
  mounted () {
    this.fetchCurrency()
  },
  watch: {
    // следим за 1 инпутом (валюта 1)
    currency1 () {
      this.amount ? this.getCurrency() : ''
    },
    // следим за 2 инпутом (валюта 2)
    currency2 () {
      this.amount ? this.getCurrency() : ''
    },
    // следим за 3 инпутом (количество - amount)
    amount () {
      this.getCurrency()
    }
  }
}
</script>

