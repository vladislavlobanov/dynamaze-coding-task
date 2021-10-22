<template>
    <div>
        <div
            class="decreaseIncreaseButtonContainer"
            @click="increase(activeEl)"
        >   
            <div
                class="decreaseIncreaseButton"
            >
                <svg
                    class="increaseDescreaseSvg"
                    width="14"
                    height="14"
                    viewBox="0 0 14 14"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <line
                        y1="7"
                        x2="14"
                        y2="7"
                        stroke="black"
                        stroke-width="2"
                    />
                    <line
                        x1="7"
                        y1="14"
                        x2="7"
                        stroke="black"
                        stroke-width="2"
                    />
                </svg>
            </div>
        </div>
        <div
            class="decreaseIncreaseButtonContainer"
            @click="decrease(activeEl)"
        >   
            <div
                class="decreaseIncreaseButton"
            >
                <svg
                    class="increaseDescreaseSvg"
                    width="14"
                    height="2"
                    viewBox="0 0 14 2"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <line
                        y1="1"
                        x2="14"
                        y2="1"
                        stroke="black"
                        stroke-width="2"
                    />
                </svg>
            </div>
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
<style scoped>

.decreaseIncreaseButtonContainer {
    height: 40.5px;
    width: 54px;
    border-radius: 20.25px;
    position:relative;
    overflow: hidden;
    cursor: pointer;
}

 .decreaseIncreaseButtonContainer::before {
    content: "";
    position: absolute;
    border: 5px solid white;
    box-sizing: border-box;
    width: 58.6px;
    bottom: 5.5px;
    transform: rotate(-25.5deg) translate(0px, -100%);
}  

.decreaseIncreaseButton {
    height: 100%;
    width: 100%;
    background: #ffffff;
    border: 2px solid #55c57a;
    box-sizing: border-box;
    border-radius: 20.25px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.increaseDescreaseSvg {
    position: absolute;
}

</style>
