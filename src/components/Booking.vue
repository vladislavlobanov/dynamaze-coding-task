<template>
    <!-- container for "Booking component" -->
    <div id="booking">
        <!-- promo image of the activity under DynAmaze logo -->
        <section />
        <!-- container with timeSlots available -->
        <div
            class="bookingOptionsContainer"
        >
            <div
                v-for="timeSlot in timeSlots"
                :key="timeSlot.id"
                class="bookingOption"
            >
                <!-- upper level of one timeSlot  -->
                <!-- onClick event - handles which timeSlot is now active, what was the last one, checking if the number of tickets should remain the same or to be set to "1" -->
                <div
                    class="smallButtonContainer"
                    @click="previousActiveEl = activeEl; activeEl = parseInt(timeSlot.id); checkCounter(previousActiveEl, activeEl)"
                >  
                    <!-- :class responsible here for switching the style of timeSlot if selected -->
                    <div
                        class="smallButton"
                        :class="(activeEl == timeSlot.id)?'active':'notActive'"
                    />
                    <!-- :class responsible here for switching the font of time and prices inside the timeSlot if selected -->
                    <div
                        class="dataInsideSmallButton"
                        :class="{whiteFont : activeEl == timeSlot.id}"
                    >
                        <div class="time">              
                            {{ timeSlot.begin }}
                        </div>
                        <!-- :class responsible here for switching the color of the middle line between time and price if selected -->
                        <div
                            class="middleLine"
                            :class="{whiteBackground : activeEl == timeSlot.id}"
                        />
                        <!-- parseFloat shows the price as a decimal with .00 -->
                        <div class="price">              
                            {{ parseFloat(timeSlot.price.amount).toFixed(2).replace(".",",") }}€
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- reponsible for showing how many tickets available, "+", "-" buttons, tickets selected, total prices to be paid, "Jetzt buchen" button -->
        <!-- :active-el passes ID of active timeSlot, :time-slots passed data of all timeSlots from App, :counter is responsilbe for showing the number of tickets selected, :increase-counter and :decrease-counter are functions to handle increase and decrease of the counter, :find-element is a function responsible for finding an object inside timeSlot by ID -->
        <prices
            :active-el="activeEl"
        
            :time-slots="timeSlots"

            :counter="counter"

            :increase-counter="increaseCounter"

            :decrease-counter="decreaseCounter"

            :find-element="findElement"
        />
    </div>
</template>

<script>
// reponsible for showing how many tickets available, "+", "-" buttons, tickets selected, total prices to be paid, "Jetzt buchen" button
import Prices from './Prices.vue';

export default {
    name: "Booking",
    components: {
        Prices,
    },
    props: {
        //timeSlots data from App
        timeSlots: {
            type: Array,
            required: true,
        },
       
    },
    data() {
        return {
            // when the app mounts, previous and current selected timeslot is the first one on the screen, number of tickets selected is "1"
            previousActiveEl: 1,
            activeEl: parseInt(this.timeSlots[0].id),
            counter: 1,
        };
    },
    methods: {
        //finds object in the array timeSlots by ID
        findElement: function(findEl) {
            return this.timeSlots.find((el) => el.id == findEl);
        },
        //increases and decreases the "Counter" aka "N Tickets" available
        increaseCounter: function() {
            this.counter++;
        },
        decreaseCounter: function() {
            this.counter--;
        },
        //handling clicking on different timeSlots, checking and resetting the number of tickets
        checkCounter: function(previousActiveEl,activeEl) {
            //user clicks on the selected timeSlot, do not do anything
            if (previousActiveEl == activeEl) return;

            // the selected number of tickets remains the same, unless there are fewer tickets in the newly selected slot than in the previous one => in this case 1 ticket will be selected.
            if (this.counter <= this.findElement(activeEl).ticketAmount) {
                this.findElement(previousActiveEl).ticketAmount = this.findElement(previousActiveEl).ticketAmount  + this.counter;
                this.findElement(activeEl).ticketAmount = this.findElement(activeEl).ticketAmount  - this.counter;
            } else {
                this.findElement(previousActiveEl).ticketAmount = this.findElement(previousActiveEl).ticketAmount  + this.counter;
                this.findElement(activeEl).ticketAmount=this.findElement(activeEl).ticketAmount - 1;
                this.counter = 1;
            }

        },
    },
};
</script>

<style scoped>
    /* container for "Booking" component */
    #booking {
        display: flex;
        flex-direction: column;
        min-height: calc(100vh - 45px);
    }
    /* show the promo image of an activity */
    section {
        width: 100vw;
        height:187px;
        background-image: url("https://firebasestorage.googleapis.com/v0/b/dynamaze---pwa-1550221436823.appspot.com/o/public%2Fimg%2Fdeals%2Ffunfussball1.png?alt=media&token=448599c6-ffb7-43f4-afc9-dfb82ce426f0");
        background-size: cover;
        background-position: center;
        border-radius: 20px 0px;
    }
    /* container with timeSlots */
    .bookingOptionsContainer {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        padding-top: 20px;
        padding-bottom: 35px;
        padding-left: 46px;
        padding-right: 37.42px;

        /* distance between timeslots if there is a large number of options (portrait only) */
        flex-flow: wrap;
    }
    /* container for one timeSlot */
    .bookingOption {
        width: fit-content;

        /* distance between timeslots if there is a large number of options (portrait only)*/
        padding-right: 10px;
        padding-bottom: 10px;
    }
    /* handinling what is inside "bookingOption" container */
    .smallButtonContainer{
        height: 60px;
        width: 69.58000183105469px;
        position:relative;
        display: flex;
        align-items: center;
        text-align: center;
        cursor: pointer;
    }
    /* white skewed diagonal line on the upper right corner */
    .smallButtonContainer::before {
        content: "";
        width: 19px;
        height: 3px;
        left: 42.58px;
        top: 0px;
        position: absolute;
        background-color: white;
        transform: skew(-45deg);
        z-index: 1;
    }
    /* white skewed diagonal line on the bottom left corner */
    .smallButtonContainer::after {
        content: "";
        width: 19px;
        height: 3px;
        left: 8px;
        top: 57px;
        position: absolute;
        background-color: white;
        transform: skew(-45deg);
    } 
    /* timeSlot button insides, including green border */
    .smallButton {
        content:"";
        height: 100%;
        width: 100%;
        border-radius: 4px;
        box-sizing: border-box;
        position: absolute;
    }
    /* representation of timeSlot when it is not selected by user */
    .notActive {
        background: rgba(255, 255, 255, 0.7);
        border: 3px solid #55C57A;
        z-index: 0;
    } 
    /* time and price representation inside timeSlot when it is not seleted. If selected only color changes, see .whiteFont class */
    .dataInsideSmallButton {
        position: absolute;
        color: #55C57A;
        font-weight: 500;
        font-size: 16px;
        width: 100%;
        line-height: 20px;
        z-index: 3;

    }
    /* line between time and price inside timeSlot if not seleted. If selected, see .whiteBackground class */
    .middleLine {
        border: 1px solid #55C57A;
        margin-left: 10%;
        margin-right: 10%;
        border-radius: 4px;
    }
    /* handles representation of timeSlot if it is selected by user*/
    .active {
        background: linear-gradient(225.08deg, #7ED56F 15.51%, #55C57A 100%);
        z-index: 2;
    }
    /* changes font color inside timeSlot if selected*/
    .whiteFont {
        color: #FFFFFF;
    }
    /* changes the color of the middle line inside timeSlot if selected*/
    .whiteBackground {
        border: 1px solid #FFFFFF;
    }
</style>
