<script setup>
    import { ref, onMounted, computed, watch } from 'vue';

    const timers = ref([])

    const time_in = ref('00:00:00')
    const timer_name = ref('')
    const input_hours = ref(0)
    const input_minutes = ref(0)
    const input_seconds = ref(0)

    const timers_asc = computed(() => timers.value.sort((a, b) => {
        return 3600 * (a.hours - b.hours) + 60 * (a.minutes - b.minutes) + (a.seconds - b.seconds)
    }))

    const addTimer = () => {

        if(input_hours.value === 0 && input_minutes.value === 0 && input_seconds.value === 0){ return }

        timers.value.push({
            hours:input_hours.value,
            minutes:input_minutes.value,
            seconds:input_seconds.value,
            name:timer_name.value,
            done: false
        })
    }

    watch(timers, newVal => {
        localStorage.setItem('timers', JSON.stringify(newVal))
    }, { deep:true })

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
    <main class="app">
        <section class="header">
            <h1>Personal Timers</h1>
        </section>
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
                            min="0" 
                            max="23" 
                            placeholder="00" 
                            v-model="input_hours">
                        <h4>h&nbsp;</h4>
                        <input 
                            type="number" 
                            min="0" 
                            max="59" 
                            placeholder="00" 
                            v-model="input_minutes">
                        <h4>m&nbsp;</h4>
                        <input 
                            type="number" 
                            min="0" 
                            max="59" 
                            placeholder="00" 
                            v-model="input_seconds">
                        <h4>s</h4>
                    </div>

                    <input type="submit" value="Add timer">
                </form>

            </section>
        </section>
        <section class="timer_list">
            <h3>Active Timers</h3>
            {{ timers }}
        </section>
    
    </main>
    

</template>

