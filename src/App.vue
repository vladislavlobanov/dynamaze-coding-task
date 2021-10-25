<template>
    <!-- container for App -->
    <div id="app">
        <!-- DynAmaze logo -->
        <header>
            <img
                class="logo"
                src="../src/assets/dynamaze_logo.png"
                alt="Logo"
            >
        </header>
        <!-- Booking component, :time-slots passes data with available timeSlots from App -->
        <booking
            :time-slots="timeSlots"
        />
    </div>
</template>

<script>
// Booking components is reponsible for showing the logo of activity, timeSlots, "+", "-" buttons, how many tickets available, how many tickets the user selected, price to be paid, and "Jetzt buchen" button. The component includes a subcomponent "Prices" to distribute this functionality between them. See Booking.vue and Prices.vue for more details
import Booking from './components/Booking.vue';

export default {
    name: "App",
    components: {
        Booking,
    },
    data: function() {
        return {
            // getting data about all timeSlots available
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
    /* importing Montserrat font, weight 400 */
    @font-face {
        font-family: Montserrat;
        src: url("../src/assets/Montserrat-Regular.ttf") format("truetype");
        font-weight: 400;
        font-style: normal;
    } 
    /* importing Montserrat font, weight 500 */
    @font-face {
        font-family: Montserrat;
        src: url("../src/assets/Montserrat-Medium.ttf") format("truetype");
        font-weight: 500;
        font-style: normal;
    } 
    /* handling body */
    body {
        box-sizing: border-box;
        margin: 0;
    }

/* IMPORTANT: GO TO MEDIA QUERY UNDER .logo FOR HANDLING IPHONE 6, 7, 8 styling */
 
    /* App component basic set-up */
    #app {
        font-family: Montserrat;
        height: 100vh;
        color:#E5E5E5;
    }
    header {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 45px;
        background: #FFFFFF;
        border-bottom: 2px solid #FF9232;
    }
    /* sizing of DynAmaze logo */
    .logo {
        width: 166px;
        height: 34px;
    }

/* MEDIA QUERY FOR HANDLING IPHONE 6, 7, 8 styling - PORTRAIT MODE ONLY */

    @media only screen 
    and (min-device-width : 375px) 
    and (max-device-width : 667px) 
    and (orientation : portrait) {
    /* App component basic set-up */
    #app {
        font-family: Montserrat;
        height: 100vh;
        color:#E5E5E5;
    }
    /* handling header which includes DynAmaze logo only */
    header {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 45px;
        background: #FFFFFF;
    }
    /* sizing of DynAmaze logo */
    .logo {
        width: 166px;
        height: 34px;
    }
    }
</style>
