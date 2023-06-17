

<script setup>
    import { computed } from '@vue/reactivity';
    import {h, readonly, ref, watch} from 'vue'
    

    const inputHours = ref(0)
    const inputMinutes = ref(0)
    const inputSeconds = ref(0)

    const hour = ref(null)
    const minute = ref(null)
    const second = ref(null)

    const time = ref(0)
    var run

    watch((inputHours), (newHours)=>{
        inputHours.value = remove_alpha_characters(newHours)
        if(inputHours.value.length > 2){
            inputHours.value = inputHours.value.slice(1)
        }
        if(Number(inputHours.value) >= 24){
            inputHours.value = '23'
        }
    })
    watch((inputMinutes), (newMinutes)=>{
        inputMinutes.value = remove_alpha_characters(newMinutes)
        if(inputMinutes.value.length > 2){
            inputMinutes.value = inputMinutes.value.slice(1)
        }
        if(Number(inputMinutes.value) >= 60){
            inputMinutes.value = '59'
        }
    })
    watch((inputSeconds), (newSeconds)=>{
        inputSeconds.value = remove_alpha_characters(newSeconds)
        if(inputSeconds.value.length > 2){
            inputSeconds.value = inputSeconds.value.slice(1)
        }
        if(Number(inputSeconds.value) >= 60){
            inputSeconds.value = '59'
        }
    })

    const start = () => {
        console.log("Start called")
        time.value = 3600 * Number(inputHours.value) + 60 * Number(inputMinutes.value) + Number(inputSeconds.value)

        hour.value.setAttribute( "readonly", true)
        minute.value.setAttribute( "readonly", true)
        second.value.setAttribute( "readonly", true)

        console.log(hour.value, minute.value, second.value)

        run = setInterval(function () {decrementTime()}, 1000)
    }

    const decrementTime = () => {
        console.log('a')
        time.value -= 1
        inputHours.value = (Math.floor(time.value / 3600)).toString()
        inputMinutes.value = (Math.floor(time.value / 60) % 60).toString()
        inputSeconds.value = (time.value % 60).toString()
        if(time.value <= 0){
            clearInterval(run)
            run = null
            hour.value.removeAttribute( "readonly")
            minute.value.removeAttribute( "readonly")
            second.value.removeAttribute( "readonly")
            console.log(hour.value, minute.value, second.value)
        }
    }


    const remove_alpha_characters = (inString) => {
        return inString.replace(/\D/g, '')
    }

</script>

<template>

    <div class="timerComp">
        <div>
            <input type="text" id="hour" ref="hour" v-model="inputHours">
            <label for="hour" class="timerLabel"> h  </label>
            <input type="text" id="minute" ref="minute" v-model="inputMinutes">
            <label for="minute" class="timerLabel"> m  </label>
            <input type="text" id="second" ref="second" v-model="inputSeconds">
            <label for="second" class="timerLabel"> s</label>
        </div>
        

        <button @click="start">Start</button>

    </div>
    

</template>