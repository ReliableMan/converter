<script setup>
import elements from '../../store/infoOptions.js';
const arr = elements.elements
</script>

<template>
  <div class="w-[330px] md:w-[344px] xl:w-[570px] min-[1600px]:w-[705px] h-[387px] md:h-[355px ] xl:h-[376px] min-[1600px]:h-[465px] bg-[#EEF5FF] mt-[17px] rounded-2xl border border-[#DFE1F0] xl:pb-12">
    <p class="w-[300px] md:w-[314px] xl:w-[522px] min-[1600px]:w-[645px] text-[13px] xl:text-[15px] min-[1600px]:text-[18px] leading-[18px] xl:leading-[20px] min-[1600px]:leading-6  px-[15px] pt-[26px] md:pt-[22px] xl:pt-[32px] xl:px-[24px] min-[1600px]:px-0 min-[1600px]:pl-[30px] text-[#0F4471] font-medium uppercase pb-[30px] md:pr-0">
      lorem ipsumdolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor:</p>
    <div class="md:flex">
      <!-- 1 потомок -->
      <div >
        <div class="flex items-center px-[15px] pb-[12px] md:pb-[25px] xl:pb-[15px] xl:px-0 xl:pl-[25px] min-[1600px]:pb-[20px] min-[1600px]:pl-[30px] "
        v-for="item in arr" :key="item.id">
          <img class="w-[7px] md:w-[8px] min-[1600px]:w-[10px]" src="../../assets/svg/Ellipse 53.svg"/>
          <p class="text-[14px] md:text-[13px] xl:text-[14px] min-[1600px]:text-[18px] leading-[18px] md:leading-[15px] xl:leading-[18px] min-[1600px]:leading-5 text-[#404456] ml-[9.5px] md:w-[200px] xl:w-[242px] min-[1600px]:w-[288px]">{{ item.title }} </p>
        </div>
      </div>
      <!-- 2 потомок -->
      <div>
        <div class="flex px-[15px] space-x-2 pb-[19.5px] md:flex-col md:space-y-2 md:space-x-0 xl:flex-row xl:space-y-2 xl:space-x-2 xl:flex-wrap min-[1600px]:space-y-3 min-[1600px]:space-x-4">
            <img class="size photo1" src="../../assets/images/mobile/img-1.jpg">
            <img class="size photo2" src="../../assets/images/mobile/img-2.jpg">
            <img class="size photo1" src="../../assets/images/mobile/img-3.jpg">
            <img class="size photo2" src="../../assets/images/mobile/img-4.jpg">
              <!-- for 1280px && 1600px-->
                <img class="xl-size" src="../../assets/images/mobile/img-1.jpg">
                <img class="xl-size ph1" src="../../assets/images/mobile/img-2.jpg">
                <img class="xl-size ph2" src="../../assets/images/mobile/img-3.jpg">
                <img class="xl-size" src="../../assets/images/mobile/img-4.jpg">
        </div>
      </div>
    </div>
   
  </div>
</template>

<style scoped>
@import '../../assets/css/info.css';
</style>
