<script>
export default {
    props: {
        totalBudget: Number
    }
}
</script>

<template>
    <h1>Total Budget</h1>
    <p>Please enter the total amount of money you feel comfortable spending for this trip.</p>
    <div class="inputs">
        <label for="total">Amount</label>
        <input type="number" min="0" step="1" id="total" v-model="totalBudget" />
    </div>
</template>
