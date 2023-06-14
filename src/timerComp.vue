<template>
    <h3>{{ name }}</h3>
    <h4>{{ hour }} hr {{ minute }} m  {{ second }} s</h4>
</template>

<script>
    import {ref, onMounted} from 'vue'
    // export default {
    //     inpTime: 10,
    //     name: 'timer',
    //     props:{
    //         inpTime: inpTime,
    //         inpName: inpName
    //     },
    //     setup(props){
    //         time = props.inpTime
    //         hour = Math.floor(time/3600)
    //         minute = Math.floor(time/60) % 60
    //         second = time % 60
    //         run = setInterval(decrementTime(time), 1000)
    //     }

    // }

    onMounted(() => {
        
    })

    const name = ref('')

    const time = ref(0)

    const hour = ref(0)
    const minute = ref(0)
    const second = ref(0)
    
    const run = ref(0)

    const decrementTime = time => {
        console.log(time)
        time -= 1
        if(time <= 0){
            clearInterval(run)
        }
    }

</script>