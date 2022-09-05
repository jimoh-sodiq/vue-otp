<template>
  <div>
    <!-- <NuxtWelcome /> -->
    <div class="w-full h-screen grid place-items-center p-4">
      <div class="max-w-[600px]">
        <h1 class="text-xl">
          Hi, I am Jimoh Sodiq and this is a demo vue.js otp input
        </h1>
        <p class="text-sm text-green mb-6">
          The source code can be found at
          <a
            href="https://github.com/jimoh-sodiq/vue-otp"
            class="text-blue-500 text-lg"
            >my github</a
          >
        </p>
        <!-- otp inputs start here -->
        <div
          class="flex items-center justify-center w-full h-full mx-auto overflow-x-hidden"
        >
          <form class="w-[650px]">
            <p class="text-[28px] font-medium text-dark">Verify Account</p>
            <p class="mb-[30px] text-[14px] font-medium text-dark">
              Please input the OTP sent to your email
            </p>
            <div class="w-full space-y-[30px]">
              <div class="grid grid-cols-6 gap-3 md:gap-6 p-2">
                <input
                  v-for="(item, index) in otp"
                  ref="inputRefs"
                  :key="index"
                  type="text"
                  class="rounded-md text-center text-green-600 md:w-[74px] md:h-16 flex items-center justify-center text-2xl md:text-[32px] font-semibold focus:outline-blue-500 outline-[1px] ring-1 ring-black/[0.12]"
                  :class="{
                    'bg-primary_light ring-primary': otp[index] !== '',
                  }"
                  :value="otp[index]"
                  @keyup="handleChange($event, index)"
                />
              </div>
              <!-- submit button -->
              <button class="w-full text-lg bg-blue-500 text-white rounded py-3 hover:bg-blue-600 transition-colors duration-300 mb-12" @click="verifyCode">Verify otp</button>
              <p class="text-lg text-green-600">otp = {{ otp }}</p>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const test = () => {
  alert("hello there");
};
const otp = ref(new Array(6).fill(""));
const inputRefs = ref([]);
onMounted(() => inputRefs.value[0].focus());
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const handleChange = (e, index: number) => {
  const newOTP = [...otp.value];
  newOTP[index] = e.target.value.substring(e.target.value.length - 1);
  otp.value = newOTP;
  if (
    (!inputRefs.value[index]?.value || inputRefs.value[index]?.value) &&
    inputRefs.value[index + 1] &&
    e.key === "ArrowRight"
  ) {
    inputRefs.value[index + 1].focus();
  }
  if (inputRefs.value[index]?.value && inputRefs.value[index + 1]) {
    inputRefs.value[index + 1].focus();
  }
  if (
    (!inputRefs.value[index]?.value || inputRefs.value[index]?.value) &&
    inputRefs.value[index - 1] &&
    e.key === "ArrowLeft"
  ) {
    inputRefs.value[index - 1].focus();
  }
  if (
    !inputRefs.value[index]?.value &&
    inputRefs.value[index - 1] &&
    e.key === "Backspace"
  ) {
    inputRefs.value[index - 1].focus();
  }
};

const verifyCode = () => {
  alert("your otp is " + otp.value)
}
</script>

<style scoped></style>
