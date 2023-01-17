<template>
  <ul class="flex items-center text-[12px] leading-[14px] font-normal text-center text-black w-full bg-gray-50 h-[40px] xl:pl-[30px] min-[1600px]:pl-[50px]">
    <li @click="addActive" class="ml-8">
        <NuxtLink to="/"  :class="{activeSt: index}" aria-current="page" class="inline-block text-gray-500 active:text-black focus:text-black">Калькулятор</NuxtLink>
    </li>
    <li @click="addActive" class="ml-7 md:ml-[30px] md:w-[86px]">
        <NuxtLink to="/second" :class="{activeSt: second}" class="inline-block text-gray-500 active:text-black focus:text-black">Курс рубля</NuxtLink>
    </li>
</ul>
</template>

<script>
export default {
  data () {
    return {
      index: false,
      second: false
    }
  },
  methods: {
    addActive (event) {
      let elements = document.querySelectorAll('ul > li > a');
      elements.forEach((el) => {
        el.classList.contains('activeSt') ? el.classList.remove('activeSt') : '';
      });
      let elem = event.target.classList;
      elem.contains('activeSt') ? '' : elem.add('activeSt');
    }
  },
  mounted () {
    if (window.location.href.includes('second')) {
      this.second = true;
      this.index = false
    } else {
      this.index = true;
      this.second = false;
    };
  }
}
</script>

<style scoped>
.activeSt {
  color: black
}
</style>
