<template>
  <div class="home">
    <form name="change-calc" @submit.prevent="calcChange(amount)">
      <input v-model="amount" placeholder="Amount"/>
      <button type="submit">Calculate</button>
      <p :key="index" v-for="(money, index) in this.output">
        {{ money }}
      </p>
    </form>
  </div>
</template>

<script>
export default {
  name: 'home',
  data: function () {
      return {
          amount: '',
          coins: [
              200,
              100,
              50,
              20,
              10,
              5,
              2,
              1
          ],
          output: []
      }
  },
  methods: {
      calcChange (amount) {
        if (amount === 0)
        {
            return [];
        }
        else
        {
            // If given amount is larger than largest coin, removes largest coin value from amount and adds to the outputted array.
            // Then runs the function again with leftover amount.
            if (amount >= this.coins[0])
            {
                let left = (amount - this.coins[0]);
                this.output.push(new Intl.NumberFormat('en-EN', {
                    style: 'currency',
                    currency: 'GBP',
                    minimumFractionDigits:2,
                    maximumFractionDigits:2
                }).format(this.coins[0] / 100));
                return [this.coins[0]].concat( this.calcChange(left));
            }
            // If given amount is NOT larger the largest coin, it removes the largest coin from the array
            // Then runs array again.
            else
            {
                this.coins.shift();
                return this.calcChange(amount);
            }
        }

      }
  }
}
</script>
