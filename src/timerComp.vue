<template>

    <input type="text" v-model="timerName" readonly="readonly" />

    <div>
        <h4>{{ hour }} : {{ minute }} : {{ second }}</h4>
    </div>   

</template>

<script>
    import {h, ref, watch} from 'vue'
    export default {
        props:{
            inpTime: Number,
            inpName: String
        },
        setup(props){



        },
        data: function () {
            return {
                time: ref(this.inpTime),
                timerName: ref(this.inpName),
                hour: ref(Math.floor(this.inpTime/3600)),
                minute: ref(Math.floor(this.inpTime/60) % 60),
                second: ref(this.inpTime % 60),
                run
            }   
        },
        mounted () {
            run = setInterval(function () {this.decrementTime()}, 1000)
            console.log(run)
        },
        // watch: {
        //     hour(val)  {
        //         this.$el.queryselector('#hour').innerText = val
        //     },

        //     minute(val) {
        //         this.$el.queryselector('#minute').innerText = val
        //     },

        //     second(val){
        //         this.$el.queryselector('#second').innerText = val
        //     }
        // },
        methods: {
            decrementTime() {
                time.value -= 1
                hour.value = Math.floor(time.value/3600)
                minute.value = Math.floor(time.value/60) % 60
                second.value = time.value % 60

                console.log(hour.value, minute.value, second.value, time.value)
                
                if(time.value <= 0){
                    clearInterval(run)
                }
            }
        }
    }

    var timerName = ref('')

    const time = ref(0)

    const hour = ref(0)
    const minute = ref(0)
    const second = ref(0)
    let run = null

    let decrementTime = () => {
        time.value -= 1
        hour.value = Math.floor(time.value/3600)
        minute.value = Math.floor(time.value/60) % 60
        second.value = time.value % 60
        if(time.value <= 0){
            clearInterval(run)
        }
    }

    
    
    

</script>