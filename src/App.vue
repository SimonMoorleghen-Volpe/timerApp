<script setup>
    import { ref, watch, createApp } from 'vue'
    
    import timerComp from './timerComp.vue'


</script>

<template>
    <section class="header">
            <h1>Personal Timers</h1>
        </section>
    <main class="app">
        <timerComp></timerComp>

    </main>
    

</template>

