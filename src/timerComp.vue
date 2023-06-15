<template>

    <input type="text" v-model="name" readonly="readonly" />

    <div class="time_select">
        <h4 id="hour">0</h4>
        <h4 id="minute">0</h4>
        <h4 id="second">0</h4>
    </div>

</template>

<script>
    import {ref, watch} from 'vue'
    export default {
        props:{
            inpTime: Number,
            inpName: String
        },
        setup(props){

            name.value = props.inpName
            time.value = props.inpTime
            
            hour.value = Math.floor(time.value/3600)
            minute.value = Math.floor(time.value/60) % 60
            second.value = time.value % 60
            run = setInterval(function() {decrementTime()}, 1000)
            // return {name, time, hour, minute, second}
        },
        data: function () {
            return {
                time: this.inpTime,
                name: this.inpName,
                hour: hour,
                minute: minute,
                second: second,

            }   
        }
    }

    const name = ref('')

    const time = ref(0)

    const hour = ref(0)
    const minute = ref(0)
    const second = ref(0)
    var run

    let decrementTime = () => {
        time.value -= 1
        hour.value = Math.floor(time.value/3600)
        minute.value = Math.floor(time.value/60) % 60
        second.value = time.value % 60
        if(time.value <= 0){
            clearInterval(run)
        }
    }

    watch(hour, (newHour)=>{
        document.getElementById('hour').innerHTML = newHour
    })

    watch(minute, (newMinute)=>{
        document.getElementById('minute').innerHTML = newMinute
    })

    watch(second, (newSecond)=>{
        document.getElementById('second').innerHTML = newSecond
    })

</script>