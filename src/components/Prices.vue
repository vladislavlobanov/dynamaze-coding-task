<template>
    <div>
        <div>
            <button @click="increase(activeEl)">
                +
            </button>
            <button @click="decrease(activeEl)">
                –
            </button>
        </div>
        <p>
            Number of tickets available:
            {{ showNumberOfTickets(activeEl) }}
        </p>
        <p>{{ counter }}</p>
        <p>{{ showPrice(activeEl) }} EUR</p>
        <button @click="bookingConfirmation(activeEl)">
            Jetzt buchen
        </button>
    </div>
</template>

<script>
export default {
    name: "Prices",
    props: {
        timeSlots: {
            type: Array,
            required: true,
        },
        activeEl: {
            type: Number,
            required: true,
        },
        counter: {
            type: Number,
            required: true,
        },
        increaseCounter: {
            type: Function,
            required: true,
        },
        decreaseCounter: {
            type: Function,
            required: true,
        },
    },
    data() {
        return {};
    },

    methods: {
        increase: function(activeEl) {
            if (
                this.timeSlots.find((el) => el.id == activeEl).ticketAmount == 0
            )
                return;

            this.increaseCounter();
            this.timeSlots.find((el) => el.id == activeEl).ticketAmount--;
        },
        decrease: function(activeEl) {
            if (this.counter == 1) return;

            this.decreaseCounter();
            this.timeSlots.find((el) => el.id == activeEl).ticketAmount++;
        },
        showNumberOfTickets: function(activeEl) {
            return this.timeSlots.find((el) => el.id == activeEl).ticketAmount;
        },
        showPrice: function(activeEl) {
            return (
                this.timeSlots.find((el) => el.id == activeEl).price.amount *
                this.counter
            );
        },
        bookingConfirmation: function(activeEl) {
            alert(
                `Booking TimeSlot at ${
                    this.timeSlots.find((el) => el.id == activeEl).begin
                }, ${this.counter} tickets at ${
                    this.timeSlots.find((el) => el.id == activeEl).price.amount
                } € succeeded`
            );
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
