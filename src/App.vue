<template>
    <!-- <p>Data:</p>
    {{ JSON.stringify(timeSlots, null, 4) }} -->
    <div id="app">
        <header>
            <img
                class="logo"
                src="../src/assets/dynamaze_logo.png"
                alt="Logo"
            >
        </header>
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
                    id: "2",
                    ticketAmount: 10,
                    begin: "11:00",
                    price: {
                        amount: 10,
                        currency: "EUR",
                    },
                },
                {
                    id: "3",
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

@font-face {
  font-family: Montserrat;
  src: url("../src/assets/Montserrat-Regular.ttf") format("truetype");
  font-weight: 400;
  font-style: normal;
} 

@font-face {
  font-family: Montserrat;
  src: url("../src/assets/Montserrat-Medium.ttf") format("truetype");
  font-weight: 500;
  font-style: normal;
} 
body {
    box-sizing: border-box;
    margin: 0;
}

#app {
    font-family: Montserrat;
    
}

header {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 45px;
}

.logo {
    width: 166px;
    height: 34px;
}
</style>
