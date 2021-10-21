<template>
    <div>
        <div
            v-for="timeSlot in timeSlots"
            :key="timeSlot.id"
        >
            <button
                :class="{ active : activeElGetterSetter == timeSlot.id }"
                @click="previousActiveEl = activeElGetterSetter; activeElGetterSetter = timeSlot.id; checkCounter(previousActiveEl, timeSlot.id)"
            >
                {{ timeSlot.begin }} {{ timeSlot.price.amount }}
            </button>
        </div>
        <prices
            v-if="activeElGetterSetter"
          
            :active-el="activeEl"
        
            :time-slots="timeSlots"

            :counter="counter"

            :increase-counter="increaseCounter"

            :decrease-counter="decreaseCounter"
        />
        <div v-else>
            Please select a timeslot
        </div>
    </div>
</template>
      <!-- v-model="activeElGetterSetter" -->
            <!-- type="number" -->
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
            previousActiveEl: 0,
            activeEl: 0,
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


        // activate:function(el){
        //     this.activeEl = el;
        // },
    },
    methods: {
        increaseCounter: function() {
            this.counter++;
        },
        decreaseCounter: function() {
            this.counter--;
        },
        checkCounter: function(previousActiveEl,activeEl) {

            if (!previousActiveEl) {
                return this.timeSlots.find((el) => el.id == activeEl).ticketAmount=this.timeSlots.find((el) => el.id == activeEl).ticketAmount - 1;
            }
           
            if (previousActiveEl && this.counter <= this.timeSlots.find((el) => el.id == activeEl).ticketAmount ) {
                this.timeSlots.find((el) => el.id == previousActiveEl).ticketAmount = this.timeSlots.find((el) => el.id == previousActiveEl).ticketAmount  + this.counter;
                this.timeSlots.find((el) => el.id == activeEl).ticketAmount = this.timeSlots.find((el) => el.id == activeEl).ticketAmount  - this.counter;
            } else {
                this.timeSlots.find((el) => el.id == previousActiveEl).ticketAmount = this.timeSlots.find((el) => el.id == previousActiveEl).ticketAmount  + this.counter;
                this.timeSlots.find((el) => el.id == activeEl).ticketAmount=this.timeSlots.find((el) => el.id == activeEl).ticketAmount - 1;
                this.counter = 1;
            }

        },
    },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .active {
    background-color:green;
    }
</style>
