<template>
    <div>
        <div class="card flex justify-center">
        <InputOtp v-model="emailotp" :length="6" size="large"/>
    </div>
    </div>
</template>

<script setup>
const emailotp=ref(null)
</script>

<style>

</style>