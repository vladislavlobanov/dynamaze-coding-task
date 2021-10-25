<template>
    <!-- "Prices" component -->
    <div id="prices">
        <!-- shows the number of tickets available -->
        <div class="ticketsNumber">
            Nur noch {{ showNumberOfTickets(activeEl) }} Tickets vorhanden.
        </div> 
        <!-- container with "+", "N Tickets", "-" button -->
        <div class="counterContainer"> 
            <!-- "+" button -->
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
            <!-- "N Tickets" element  -->
            <div class="numberOfTickets">
                {{ counter }} {{ counter > 1 ? "Tickets" : "Ticket" }}
            </div>
            <!-- "-" button -->
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
        <!-- Total price element -->
        <div class="totalPrice">
            <!-- handles currency representation on the screen ,00 -->
            {{ parseFloat(showPrice(activeEl)).toFixed(2).replace(".",",") }}€
        </div>
        <!-- "Jetz buchen" button -->
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
        //timeSlots data from App
        timeSlots: {
            type: Array,
            required: true,
        },
        //selected timeSlot by id
        activeEl: {
            type: Number,
            required: true,
        },
        //number of tickets selected
        counter: {
            type: Number,
            required: true,
        },
        //increases the counter of tickets
        increaseCounter: {
            type: Function,
            required: true,
        },
        //decreease the counter of tickets 
        decreaseCounter: {
            type: Function,
            required: true,
        },
        //finds object in the array timeSlots by ID, defined in "Booking component"
        findElement: {
            type: Function,
            required: true,
        },
    },
    //after mounting, immedeatly decrease the number of tickets by one for the first selected timeSlot on the screen 
    mounted() {
        this.findElement(this.activeEl).ticketAmount--;
    },
    methods: {
        //handles "+" button, including checking if there are tickets available
        increase: function(activeEl) {
            if (!this.findElement(activeEl).ticketAmount) return;

            this.increaseCounter();
            this.findElement(activeEl).ticketAmount--;
        },
        //handles "-" button, including checking if there are tickets available
        decrease: function(activeEl) {
            if (this.counter == 1) return;

            this.decreaseCounter();
            this.findElement(activeEl).ticketAmount++;
        },
        //shows the total number of tickets available on the screen
        showNumberOfTickets: function(activeEl) {
            return this.findElement(activeEl).ticketAmount+this.counter;
        },
        //shows the total price to be paid by user
        showPrice: function(activeEl) {
            return (
                this.findElement(activeEl).price.amount *
                this.counter
            );
        },
        //handles clicking on the button "Jetzt Buchen" and sending this data to server (future option)
        bookingConfirmation: function(activeEl) {
            alert(
                `Booking TimeSlot at ${
                    this.findElement(activeEl).begin
                }, ${this.counter} tickets at ${
                    this.showPrice(activeEl)} € succeeded`
            );
        },
    },
};
</script>

<style scoped>
    /* container for the Prices component */
    #prices {
        flex-grow: 1;
        display: flex; 
        flex-direction: column;
    }
    /* properties for showing how many tickets are still available */
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
    /* container that includes "+", "N Tickets", "-" elements */
    .counterContainer {
        display: flex;
        align-items: center;
        padding-left: 45px; 
        padding-right: 45px;
        justify-content: center;
    }
    /* container for "+" and "-" buttons */
    .decreaseIncreaseButtonContainer {
        height: 40.5px;
        width: 54px;
        border-radius: 20.25px; 
        position:relative;
        overflow: hidden;
        cursor: pointer;
    }
    /* diagonal white line from left bottom corner to the top righ on "+", "-" buttons */
    .decreaseIncreaseButtonContainer::before {
        content: "";
        position: absolute;
        border: 5px solid white;
        box-sizing: border-box;
        width: 58.6px;
        bottom: 5.5px;
        transform: rotate(-25.5deg) translate(0px, -100%);
    }  
    /* positioning "-" to the left side, avoids jumping behavior if the size of "number of Tickets" changes */
    .decreaseIncreaseButtonContainer.leftButton {
        margin-right: auto;
    }
    /* reponsible for styling "N Tickets" between "+", "-" buttons */
    .numberOfTickets {
        font-family: Montserrat;
        font-style: normal;
        font-weight: normal;
        font-size: 20px;
        color: #222222;
    }
    /* positioning "+" to the right side, avoids jumping behavior if the size of "number of Tickets" changes */
    .decreaseIncreaseButtonContainer.rightButton {
        margin-left: auto;
    }
    /* styling of the "+", "-" buttons */
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
    /* positioning of "+", "-" SVGs */
    .increaseDescreaseSvg {
        position: absolute;
    }
    /* styling of total price to be paid by user */
    .totalPrice{
        padding-top: 17.5px;
        display: flex;
        justify-content: center;
        font-style: normal;
        font-weight: bold;
        font-size: 18px;
        color: #55C57A;
    }
    /* positioning of "Jetz buchen" elements */
    .positionBuchenGroup {
        height: 100%;
        width: 100%;
        flex-grow:1;
        display: flex;
        justify-content: center;
        align-items: flex-end;
    }
    /* padding for "Jetzt buchen" */
    .buchenContainer {
        padding-bottom: 29px;
        padding-top: 9px;
    }
    /* styling for "Jetzt buchen" button*/
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
    /* styling for "Jetzt buchen" button's text*/
    .textBuchen {
        font-family: Montserrat;
        font-style: normal;
        font-weight: 500;
        font-size: 16px;
        color: #FFFFFF;
        cursor: pointer;
    }
</style>
