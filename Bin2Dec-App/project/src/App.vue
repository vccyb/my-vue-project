<template>
  <div>
    <h1>Bin2Dec</h1>
    <p>请输入二进制数字，获取对应的十进制转换</p>
    <p :class="[flag ? 'text-green-500' : 'text-red-500', 'font-bold']">
      tips:
      {{ flag ? "您的二进制对应的十进制显示在下方" : "请输入正确的二进制" }}
    </p>
    <input
      type="text"
      placeHolder="请输入二进制"
      class="border-4 w-[300px] h-[60px] m-2 rounded outline-0 indent-2 border-purple-500 text-2xl"
      v-model="bin"
      maxLength="16"
    />
    <p class="mt-2 bold text-4xl">
      {{ flag ? dec : "" }}
    </p>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from "vue";

let bin = ref<number>();
let dec = ref<number>();
let flag = ref<boolean>(true);

const bin2dec = (bin: string): string => {
  return parseInt(bin, 2).toString();
};

watch(bin, (newVal, oldVal) => {
  flag.value = true;
  newVal = newVal.trim();
  const checkArr = [0, 1];
  if (newVal === "") flag.value = false;
  for (let i = 0; i < newVal.length; i++) {
    if (!checkArr.includes(Number(newVal[i]))) {
      flag.value = false;
    }
  }
  dec.value = bin2dec(newVal);
});
</script>

<style scoped></style>
