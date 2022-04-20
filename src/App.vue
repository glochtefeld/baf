<script>
export default {
    data() {
        return {
            tBudget: 0,

            gasDist: 100,
            gasPrice: 3.90,
            gasEff: 30,
            gasCarpool: 1,
            otherTravel: 0,

            sharedMeal: 36,
            byob: 0,

        }
    },
    methods: {
        getFinalGas() {
            return ((this.gasDist * this.gasPrice / this.gasEff)/this.gasCarpool) + this.otherTravel;
        },
        getFinalMeal() {
            return this.sharedMeal + this.byob;
        },
        getCabinContrib() {
            return this.tBudget - this.getFinalGas() - this.getFinalMeal();
        }
    }
}
</script>

<template>
    <div class="totalB">
        <h1>Total Budget</h1>
        <p>Please enter the total amount of money you feel comfortable spending for this trip.</p>
        <div class="inputs">
            <label for="total">Amount</label>
            <input type="number" min="0" step="1" id="total" v-model="tBudget" />
        </div>
    </div>
    <div class="travelB">
        <h2>Travel Costs (one way)</h2>
        <p>To estimate travel costs, use the following benchmarks:</p>
        <ul>
            <li>From the twin cities: 100 mi</li>
            <li>From Grinnel: 250 mi</li>
            <li>From Chicago: 400 mi</li>
        </ul>
        <div class="inputs">
            <label for="gasDist">Distance Driven</label>
            <input id="gasDist" type="number" min="0" step="0.5" v-model="gasDist">
            <label for="gasPrice">Price of Gas per Gallon</label>
            <input id="gasPrice" type="number" min="0.01" step="0.01" v-model="gasPrice">
            <label for="gasEff">Fuel Efficiency</label>
            <input id="gasEff" type="number" min="1" step="1" v-model="gasEff">
            <label for="gasCarpool">Number of people carpooling</label>
            <input id="gasCarpool" type="number" min="1" step="1" v-model="gasCarpool">
            <label for="otherTravel">Other Travel Costs (snacks, etc)</label>
            <input id="otherTravel" type="number" min="0" step="0.01" v-model="otherTravel">
        </div>
    </div>
    <div class="foodB">
        <h2>Food Costs</h2>
        <small>Shared food cost is estimated at $36 for the weekend.</small>
        <div class="inputs">
            <label for="sharedFood">Shared Meal Costs</label>
            <input id="sharedFood" type="number" min="0" step="1" v-model="sharedMeal" disabled>
            <label for="byobFood">BYOB Budget</label>
            <input id="byobFood" type="number" min="0" step="1" v-model="byob">
        </div>
    </div>

    <div class="finalB">
        <h1>Final Budget Breakdown</h1>
        <p>Your final travel cost is ${{getFinalGas().toFixed(2)}}.</p>
        <p>Your final food contribution will be ${{getFinalMeal()}}.</p>
        <p>Your amount you can contribute towards the cabin is ${{getCabinContrib().toFixed(2)}}. <i v-if="getCabinContrib() < 0">Damn! You're making money ON TOP of money!</i> Please <b>PUT THIS NUMBER</b> in the google form.</p>
    </div>
</template>

<style>
@import './assets/base.css';

#app {
    max-width: 1280px;
    margin: 0 auto;
    padding: 25%;

    font-weight: normal;
}

div {
    line-height: 1.5;
}
.totalB { grid-area: 1 / 1 / 2 / 3; }
.travelB { grid-area: 2 / 1 / 4 / 2; }
.foodB { grid-area: 2 / 2 / 4 / 3; }
.finalB { grid-area: 4 / 1 / 5 / 3; }

.inputs {
    display: flex;
    flex-direction:column;
}


@media (min-width: 1024px) {
    body {
        display: flex;
        place-items: center;
    }

    #app {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-template-rows: repeat(4, 1fr);
        /* grid-template-columns: 1fr 1fr; */
        padding: 0 1rem;
        grid-gap: 50px;
    }

    header {
        display: flex;
        place-items: center;
        padding-right: calc(var(--section-gap) / 2);
    }

    header .wrapper {
        display: flex;
        place-items: flex-start;
        flex-wrap: wrap;
    }

    .logo {
        margin: 0 2rem 0 0;
    }
}
</style>
