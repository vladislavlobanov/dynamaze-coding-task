<template>
    <div id="prices">
        <div class="ticketsNumber">
            Nur noch {{ showNumberOfTickets(activeEl) }} vorhanden.
        </div> 
        <div class="counterContainer"> 
            <div
                class="decreaseIncreaseButtonContainer leftButton"
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
            <div class="numberOfTickets">
                {{ counter }} {{ counter > 1 ? "Tickets" : "Ticket" }}
            </div>

            <div
                class="decreaseIncreaseButtonContainer rightButton"
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
        </div>
        
        
        <div class="totalPrice">
            {{ parseFloat(showPrice(activeEl)).toFixed(2) }}€
        </div>
        <div class="positionBuchenGroup">
            <div class="buchenContainer">
                <div
                    class="buchen"
                    @click="bookingConfirmation(activeEl)"
                >
                    <div class="textBuchen">
                        Jetzt buchen
                    </div>
                </div>
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
        findElement: {
            type: Function,
            required: true,
        },
    },
    mounted() {
        this.findElement(this.activeEl).ticketAmount--;
    },
    methods: {
        increase: function(activeEl) {
            if (!this.findElement(activeEl).ticketAmount) return;

            this.increaseCounter();
            this.findElement(activeEl).ticketAmount--;
        },
        decrease: function(activeEl) {
            if (this.counter == 1) return;

            this.decreaseCounter();
            this.findElement(activeEl).ticketAmount++;
        },
        showNumberOfTickets: function(activeEl) {
            return this.findElement(activeEl).ticketAmount+this.counter;
        },
        showPrice: function(activeEl) {
            return (
                this.findElement(activeEl).price.amount *
                this.counter
            );
        },
        bookingConfirmation: function(activeEl) {
            alert(
                `Booking TimeSlot at ${
                    this.findElement(activeEl).begin
                }, ${this.counter} tickets at ${
                    this.findElement(activeEl).price.amount
                } € succeeded`
            );
        },
    },
};
</script>

<style scoped>
    #prices {
        flex-grow: 1;
        display: flex; 
        flex-direction: column;
    }
    .ticketsNumber {
        display: flex; 
        justify-content: center;
        padding-bottom: 16px;
        font-family: Montserrat;
        font-style: normal;
        font-weight: normal;
        font-size: 16px;
        color: #222222;
    }

    .counterContainer {
        display: flex;
        align-items: center;
        padding-left: 45px; 
        padding-right: 45px;
        justify-content: center;
    }

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

    .decreaseIncreaseButtonContainer.leftButton {
        margin-right: auto;
    }

    .numberOfTickets {
        font-family: Montserrat;
        font-style: normal;
        font-weight: normal;
        font-size: 20px;
    }

    .decreaseIncreaseButtonContainer.rightButton {
        margin-left: auto;
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

    .totalPrice{
        padding-top: 17.5px;
        display: flex;
        justify-content: center;
        font-style: normal;
        font-weight: bold;
        font-size: 18px;
        color: #55C57A;
    }

    .positionBuchenGroup {
        height: 100%;
        width: 100%;
        flex-grow:1;
        display: flex;
        justify-content: center;
        align-items: flex-end;
    }

    .buchenContainer {
        padding-bottom: 29px;
        padding-top: 9px;
    }

    .buchen{
        width: 337.5px;
        height: 38px;
        border-radius: 10px;
        background: linear-gradient(87.6deg, #FF9232 -28.36%, #FAC162 104.8%);
        box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.1);
        display: flex; 
        justify-content: center;
        align-items: center;
    }

    .textBuchen {
        font-family: Montserrat;
        font-style: normal;
        font-weight: 500;
        font-size: 16px;
        color: #FFFFFF;
        cursor: pointer;
    }
</style>
