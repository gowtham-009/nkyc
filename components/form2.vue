<template>

    <div class="p-1">
        <div style="border: 1px solid red;" :style="{ height: deviceHeight * 0.09 + 'px' }"></div>
        <div class="flex" style="border: 1px solid red;" :style="{ height: deviceHeight * 0.80 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk" style="border: 1px solid black;">
                <div class="w-full bg-slate-500" style="height: 500px;"></div>
            </div>
            <div class="w-1/2 p-2 flex items-center md " style="border: 1px solid black;">
                <div class="w-full p-2" >
                    <div class="flex flex-col gap-1 disabled ">
                        <mobileinput/>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                        <phoneotp/>
                        <p class="text-right">Resend</p>
                    </div>
                    <div class="flex flex-col gap-1 mt-2 disabled ">
                        <emailinput/>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                        <emailotp/>
                        <p class="text-right">Resend</p>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                        <referalcode/>
                    </div>
                </div>
            </div>
        </div>
        <div class="flex" style="border: 1px solid red;" :style="{ height: deviceHeight * 0.09 + 'px' }">
            <div class="w-1/2 p-1 flex items-center">
            </div>
            <div class="w-1/2 p-1 flex justify-between items-center" >
                <button type="button" class="rounded-md bg-indigo-500  px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-500">Preview</button>

                <button type="button" class="rounded-md bg-indigo-500  px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-500">Next</button>
            </div>
        </div>

    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import mobileinput from '~/components/forminputs/mobileinput.vue';
import emailinput from '~/components/forminputs/emailinput.vue';
import checkbox from '~/components/forminputs/remembercheckbox.vue';
import phoneotp from '~/components/forminputs/phoneotp.vue';

import emailotp from '~/components/forminputs/emailotp.vue';

import referalcode from '~/components/forminputs/referalcode.vue';
const checked = ref(false);
const deviceHeight = ref(0);
const deviceWidth=ref(0)

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});
</script>
<style>
@import url("~/assets/css/form1.css");
.disabled {
  pointer-events: none;
  opacity: 0.5;
}
</style>
