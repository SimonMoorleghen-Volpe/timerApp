<script setup>
    import { createElementVNode, ref, watch } from 'vue'
    import timerComp from './timerComp.vue'

    const timers = ref([])
    const timer_name = ref('')
    const input_hours = ref(0)
    const input_minutes = ref(0)
    const input_seconds = ref(0)
    var id = 0

    const addTimer = () => {
        if(input_hours.value === 0 && input_minutes.value === 0 && input_seconds.value === 0){ return }

        // if(timers.value.length > 0){ return }
        var newNode = createElementVNode(timerComp)
        newNode.time = input_hours.value * 3600 + input_minutes.value * 60 + input_seconds.value
        newNode.name = timer_name.value
        timers.value.push( {
            name: timer_name.value,
            time: input_hours.value * 3600 + input_minutes.value * 60 + input_seconds.value,
            ID: id
        })
        id += 1

    }


    watch(input_hours, (newHour) => {
        if(typeof(newHour) == "string"){
            input_hours.value = 0
        }
        if(newHour > 23){
            input_hours.value = 23
        } else if(newHour < 0){
            input_hours.value = 0
        }
    })

    watch(input_minutes, (newMinute) => {
        if(typeof(newMinute) == "string"){
            input_minutes.value = 0
        }
        if(newMinute > 59){
            input_minutes.value = 59
        } else if(newMinute < 0){
            input_minutes.value = 0
        }
    })

    watch(input_seconds, (newSecond) => {
        if(typeof(newSecond) == "string"){
            input_seconds.value = 0
        }
        if(newSecond > 59){
            input_seconds.value = 59
        } else if(newSecond < 0){
            input_seconds.value = 0
        }
    })

</script>

<template>
    <section class="header">
            <h1>Personal Timers</h1>
        </section>
    <main class="app">
        
        <section class="timer_block">
            <section class="create_timer">
                <form @submit.prevent="addTimer">  

                    <h3>What is the timer for?</h3>

                    <input type="text" 
                    placeholder="e.g. work on project"
                    v-model="timer_name" />
                    <h3> Enter the duration.</h3>
                    <div class="time_select">
                        <input 
                            type="number" 
                            placeholder="00" 
                            v-model="input_hours">
                        <h4>h&nbsp;</h4>
                        <input 
                            type="number" 
                            placeholder="00" 
                            v-model="input_minutes">
                        <h4>m&nbsp;</h4>
                        <input 
                            type="number" 
                            placeholder="00" 
                            v-model="input_seconds">
                        <h4>s</h4>
                    </div>
                  
                    <input type="submit" value="Add Timer" />
                </form>

            </section>
        </section>
        <section class="timer_list">
            <h3>Active Timer</h3>

            <div v-for="timer in timers">
                <timerComp 
                    :key="timer.ID"
                    :inpName="timer.name"
                    :inpTime="timer.time"
                />
            </div>
            

            


        </section>
    
    </main>
    

</template>

