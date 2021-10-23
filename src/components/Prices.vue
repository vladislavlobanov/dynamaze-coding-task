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
        <div
            class="buchen"
            @click="bookingConfirmation(activeEl)"
        >
            <div class="textBuchen">
                Jetzt buchen
            </div>
        </div>
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

.buchen{
    position: absolute;
    width: 337.5px;
    height: 38px;
    padding: 9px, 76px, 9px, 76px;
    border-radius: 10px;
    background: linear-gradient(87.6deg, #FF9232 -28.36%, #FAC162 104.8%);
    box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.1);
    display: flex; 
    flex-direction: row;
    justify-content: center;
    align-items: center;
   
}

.textBuchen {
    font-family: Montserrat;
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 20px;
    color: #FFFFFF;
    cursor: pointer;
}

</style>
