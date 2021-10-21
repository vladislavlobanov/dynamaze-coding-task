<template>
    <!-- <p>Data:</p>
    {{ JSON.stringify(timeSlots, null, 4) }} -->
    <div id="app">
        <booking
            :time-slots="timeSlots"
        />
        <!-- <prices
            v-if="active_el"
            
            :time-slots="timeSlots"
        />
        <div v-else>
            Please select a timeslot
        </div> -->
    </div>
</template>

<script>
import Booking from './components/Booking.vue';


export default {
    name: "App",
    components: {
        Booking,
        // Prices,

    },
    data: function() {
        return {
            timeSlots: [
                {
                    id: "1",
                    ticketAmount: 10,
                    begin: "10:00",
                    price: {
                        amount: 10,
                        currency: "EUR",
                    },
                },
                {
                    id: "2",
                    ticketAmount: 5,
                    begin: "11:00",
                    price: {
                        amount: 10,
                        currency: "EUR",
                    },
                },
            ],
           
        };
    },
    
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
