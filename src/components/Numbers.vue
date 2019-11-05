<template>
  <div  id="numbers">
    <div class="number" :id="'number-'+number" v-for="number in n()" :key="number" @mouseover="hov(number)" @mouseout="reset" @click="pick">
      {{number}}
    </div>
  </div>
</template>

<script>
export default {
  data()
  {
    return {
      limit: this.$parent.limit,
      numbers: []
    }
  },
  watch: {
    ['$parent.limit'](newLimit)
    {
      this.limit = newLimit;
    }
  },
  methods: {
    n()
    {
      let numbers = [];
      for(var i = 0; i <= this.limit; i++) //  included the value in the input box as opposed to stopping at one below it
      {
        numbers = [...numbers, i];
      }
      // replaced numbers.sort(() => Math.random() - 0.5) with a Fisher-Yates sort as it gives a better random output
      for (let i = numbers.length - 1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1));
    [numbers[i], numbers[j]] = [numbers[j], numbers[i]];
  }
  return numbers
    },
    hov(number)
    {
      const nums = document.querySelectorAll('.number');


      for(let i = 0; i < nums.length; i++)
      {
        const num = nums[i].textContent.trim();
        // differentiated between the selected number and it's divisors
        if(number % num === 0 && number >  num)
        {
          nums[i].classList.add('active')

        }
        if(number ===  parseInt(num))
        {
          nums[i].classList.add('chosen')

        }
      }
    },
    reset()
    {
      const nums = document.querySelectorAll('.number');
      nums.forEach(num => num.classList.remove('active'))
      nums.forEach(num => num.classList.remove('chosen'))
    },
    //lets you click on a number to make that the new number of randomly ordered numbers
    pick(number){
      this.limit = number.path[0].innerText
      this.$emit('clicked', this.limit)

    }
  }
}
</script>

<style scoped>

  *{
  font-family: "Helvetica Neue";
  }

  #numbers{
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;

  }

	.number {
    width: 2em;
    height: 2em;
		padding: 5px;
		background-color: rgba(0,0,0,0);
		margin: 0.5em;
    font-size: 2em;
    color: white;
    border: 2px  solid  white;
    text-align: center;
    line-height: 2em;
    box-shadow: 8px 8px rgba(0,0,0,0.4);


	}

	.active {
		background-color: red;
    transition: 2s;
	}
  .chosen {
		background-color: blue;
    transition: 2s;
	}

</style>
