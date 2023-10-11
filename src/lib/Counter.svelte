 <script>
  let baseCurrency = 'USD';
  let targetCurrency = 'RUB';
  let amountToConvert = 1;
  let convertedAmount = 0;

  const updateConversion = async () => {
    const response = await fetch(`https://api.exchangerate-api.com/v4/latest/${baseCurrency}`);
    const data = await response.json();
    const rate = data.rates[targetCurrency];
    convertedAmount = amountToConvert * rate;
  };

  $: {
    updateConversion();
  }
  const changeF = (value) => {
    targetCurrency = value
    updateConversion()
  }
  const changS = (value) => {
    baseCurrency = value
    updateConversion()
  }
</script>

<div class="currency-converter">
  <h1>Currency Converter</h1>
  <div class="input-fields">
    <label for="baseCurrency">Base Currency:</label>
    <input type="text" id="baseCurrency" bind:value={baseCurrency} />

    <label for="targetCurrency">Target Currency:</label>
    <input type="text" id="targetCurrency" bind:value={targetCurrency} on:change={(e)=> changeF(e.target.value)} />

    <label for="amountToConvert">Amount to Convert:</label>
    <input type="number" id="amountToConvert" bind:value={amountToConvert} on:change={(e)=> changS(e.target.value)} />
  </div>
  <div class="result">
    <p>
      {amountToConvert} {baseCurrency} is equal to {convertedAmount.toFixed(5)} {targetCurrency}
    </p>
  </div>
</div>

<style>
  .currency-converter {
    font-family: Arial, sans-serif;
    text-align: center;
  }

  .input-fields {
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }

  input {
    margin: 0 10px;
    padding: 5px;
  }

  .result {
    margin-top: 20px;
  }
</style>
