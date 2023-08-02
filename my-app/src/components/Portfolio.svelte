<script>

    import data from '../data.js';

    let denomination = 'USD';
    let filter = 'crypto';

    function selectCurrency(Event) {
        denomination = Event.target.value;
    }

    function filterAssets(event) {
        filter = event.target.value;
    }
    
</script>

<style>

</style>

<div>
    <h1>Finances</h1>
    <select id="currencyDropdown" on:change={selectCurrency}>
        <option value="USD">US Dollar</option>
        <option value="AUD">AU Dollar</option>
        <option value="BTC">Bitcoin</option>
    </select>
    <select id="filterDropdown" on:change={filterAssets}>
        <option value="all">All</option>
        <option value="crypto">Crypto</option>
        <option value="stocks">Stocks</option>
        <option value="cash">Cash</option>
    </select>
    <div>
        <table>
            <table>
                <thead>
                  <tr>
                    <th>Ticker</th>
                    <th>Amount</th>
                    <th>Price</th>
                  </tr>
                </thead>
                <!-- Display all crypto -->
                <tbody>
                  {#each data.crypto as item}
                    <tr>
                      <td>{item.ticker}</td>
                      <td>{item.amount}</td>
                      <td>{item.price}</td>
                    </tr>
                  {/each}
                </tbody>
                <!-- Display all stocks -->
                <tbody>
                    {#each data.stocks as item}
                      <tr>
                        <td>{item.ticker}</td>
                        <td>{item.amount}</td>
                        <td>{item.price}</td>
                      </tr>
                    {/each}
                  </tbody>
                  <!-- Display all cash -->
                  <tbody>
                    {#each data.cash as item}
                      <tr>
                        <td>{item.ticker}</td>
                        <td>{item.amount}</td>
                        <td>{item.price}</td>
                      </tr>
                    {/each}
                  </tbody>
              </table>
        </table>

    </div>
</div>
