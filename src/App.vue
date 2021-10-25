<template>
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
    </div>
</template>

<script>
import Booking from './components/Booking.vue';


export default {
    name: "App",
    components: {
        Booking,
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

    /* @media only screen 
    and (min-device-width: 375px) 
    and (max-device-width: 667px) 
    and (-webkit-min-device-pixel-ratio: 2) { 
    } */
        #app {
            font-family: Montserrat;
            height: 100vh;
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
