<template>
    <!-- <h3>{{ name }}</h3> -->
    <!-- <h4>{{ hour.value }} hr {{ minute.value }} m  {{ second.value }} s</h4> -->
    <h4>{{ time.value }}</h4>
</template>

<script>
    import {ref, onMounted} from 'vue'
    export default {
        props:{
            inpTime: Number,
            inpName: String
        },
        setup(props){
            console.log(props.inpTime)
            console.log(props.inpName)
            // name = props.inpName
            time.value = props.inpTime
            hour = Math.floor(time.value/3600)
            minute = Math.floor(time.value/60) % 60
            second = time.value % 60
            setInterval(function () {decrementTime(time)}, 1000)
        }

    }

    const name = ref('test')

    const time = ref(0)

    let hour = ref(0)
    let minute = ref(0)
    let second = ref(0)

    let decrementTime = time => {
        console.log(time.value, hour, minute, second )
        time.value -= 1
        if(time <= 0){
            clearInterval(run)
        }
    }

</script>