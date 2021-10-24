<template>
    <div>
        <section />
        <div
            class="bookingOptionsContainer"
        >
            <div
                v-for="timeSlot in timeSlots"
                :key="timeSlot.id"
                class="bookingOption"
            >
                <div
                    class="smallButtonContainer"
                    @click="previousActiveEl = activeElGetterSetter; activeElGetterSetter = timeSlot.id; checkCounter(previousActiveEl, timeSlot.id)"
                >  
                    <div
                        class="smallButton"
                        :class="(activeElGetterSetter == timeSlot.id)?'active':'notActive'"
                    />
                    <div
                        class="dataInsideSmallButton"
                        :class="{whiteFont : activeElGetterSetter == timeSlot.id}"
                    >
                        <div class="time">              
                            {{ timeSlot.begin }}
                        </div>
                        <div
                            class="middleLine"
                            :class="{whiteBackground : activeElGetterSetter == timeSlot.id}"
                        />
                        <div class="price">              
                            {{ timeSlot.price.amount }} €
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <prices
            :active-el="activeEl"
        
            :time-slots="timeSlots"

            :counter="counter"

            :increase-counter="increaseCounter"

            :decrease-counter="decreaseCounter"
        />
    </div>
</template>
<script>
import Prices from './Prices.vue';

export default {
    name: "Booking",
    components: {
        Prices,
    },
    props: {
        timeSlots: {
            type: Array,
            required: true,
        },
       
    },
    data() {
        return {
            previousActiveEl: 1,
            activeEl: parseInt(this.timeSlots[0].id),
            counter: 1,
        };
    },
    computed:{

        activeElGetterSetter: {
            // getter
            get: function () {
                return this.activeEl;
            },
            // setter
            set: function (el) {
                this.activeEl = parseInt(el);
            },
        },
    },

    methods: {

        findElement: function(findEl) {
            return this.timeSlots.find((el) => el.id == findEl);
        },

        increaseCounter: function() {
            this.counter++;
        },
        decreaseCounter: function() {
            this.counter--;
        },
        checkCounter: function(previousActiveEl,activeEl) {
            if (previousActiveEl == activeEl) return;

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


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    section {
        width: 100vw;
        height:187px;
        background-image: url("https://firebasestorage.googleapis.com/v0/b/dynamaze---pwa-1550221436823.appspot.com/o/public%2Fimg%2Fdeals%2Ffunfussball1.png?alt=media&token=448599c6-ffb7-43f4-afc9-dfb82ce426f0");
        background-size: cover;
        background-position: center;
        border-radius: 20px 0px;
    }

    .bookingOptionsContainer {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        padding-top: 10px;
        padding-bottom: 35px;
        padding-left: 46px;
        padding-right: 37.42px;
    }
    .bookingOption {
        width: fit-content;
    }

    .smallButtonContainer{
        height: 60px;
        width: 69.58000183105469px;
        position:relative;
        display: flex;
        align-items: center;
        text-align: center;
        cursor: pointer;
    }

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

    .smallButton {
        content:"";
        height: 100%;
        width: 100%;
        border-radius: 4px;
        box-sizing: border-box;
        position: absolute;
    }

    .notActive {
        background: rgba(255, 255, 255, 0.7);
        border: 3px solid #55C57A;
        z-index: 0;
    } 

    .dataInsideSmallButton {
        
        position: absolute;
        color: #55C57A;
        font-weight: 500;
        font-size: 16px;
        width: 100%;
        line-height: 20px;
        z-index: 3;

    }

    .middleLine {
        border: 1px solid #55C57A;
        margin-left: 10%;
        margin-right: 10%;
        border-radius: 4px;
    }
  
    .active {
        background: linear-gradient(225.08deg, #7ED56F 15.51%, #55C57A 100%);
        z-index: 2;
    }

    .whiteFont {
        color: #FFFFFF;
    }

    .whiteBackground {
        border: 1px solid #FFFFFF;
    }
    

</style>
