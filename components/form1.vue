<template>
<Toast position="top-left" group="tl" />
    <div class="p-1">
        <div class="bg-indigo-500" :style="{ height: deviceHeight * 0.10 + 'px' }"></div>
        <div class="flex" style="border: 1px solid red;" :style="{ height: deviceHeight * 0.80 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk" style="border: 1px solid black;">
                <div class="w-full bg-slate-500" style="height: 500px;"></div>
            </div>
            <div class="w-1/2 p-2 flex items-center md " style="border: 1px solid black;">
                <div class="w-full p-2" >
                    <div class="flex flex-col gap-1">
                        <mobileinput  v-model="phoneNumber"/>
                    </div>
                    <div class="flex flex-col gap-1 mt-6">
                        <emailinput v-model="emailID"/>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                      <div class="flex gap-2">
                        <checkbox  v-model="remchecked"/>
                      </div>
                    
                    </div>
                </div>
            </div>
        </div>

        <div class="flex" style="border: 1px solid red;" :style="{ height: deviceHeight * 0.10 + 'px' }">
            <div class="w-1/2 p-1 dk"></div>
            <div class="w-1/2 p-1 flex justify-center items-center md" >
                <button type="button" @click="formvalidation()" class="rounded-md bg-indigo-500 w-full px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-500">Sign up</button>
            </div>
        </div>

    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import mobileinput from '~/components/forminputs/mobileinput.vue';
import emailinput from '~/components/forminputs/emailinput.vue';
import checkbox from '~/components/forminputs/remembercheckbox.vue';
import { createtoken } from '@/composables/globaltoken';
import { useUrl } from '@/composables/useUrl';
import { useToast } from 'primevue/usetoast';

const emit = defineEmits(['updateDiv']);
const toast = useToast();
const { val } = useUrl();
const token = ref(null);
const phoneNumber = ref('');
const emailID = ref('');
const remchecked=ref('')

onMounted(async () => {
    token.value = await createtoken();
});


const deviceHeight = ref(0);
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;

    });
});

const formvalidation=()=>{
   if(!phoneNumber.value){
    toast.add({ severity: 'error', summary: 'error Message', detail: 'Phone no is required', group: 'tl', life: 3000 });
   }
   else if(!emailID.value){
    toast.add({ severity: 'error', summary: 'error Message', detail: 'Email ID is required', group: 'tl', life: 3000 });
   }
   else if(!remchecked.value){
    toast.add({ severity: 'error', summary: 'error Message', detail: 'Please click your checkbox', group: 'tl', life: 3000 });
   }
   else{
   
    signup()
   }
}


const signup=async()=>{
    
   
    const apiUrl=val.value+'signup.php'
    const formdata=new FormData()
    formdata.append('mobileno',phoneNumber.value)
    formdata.append('emailid', emailID.value)
    formdata.append('token', token.value.token)

  if(token.value.token){
    try {
        const response=await fetch(apiUrl,{
            method:'POST',
            body:formdata
        })
        if(!response.ok){
            throw new Error(`HTTP error! Status: ${response.status}`);
        }
        else{
            const data=await response.json()
            if(data.status=='ok'){
                toast.add({ severity: 'success', summary: 'success Message', detail: data.message, group: 'tl', life: 3000 });
                emit('updateDiv', 'div2');
                
            }
            else{
                toast.add({ severity: 'error', summary: 'Error Message', detail: data.message, group: 'tl', life: 3000 });
            }
        }
    } catch (error) {
        console.log(error)
    }
  }
}

</script>
<style>
   @import url("~/assets/css/form1.css");
</style>
