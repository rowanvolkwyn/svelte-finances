<script>

    import data from '../data.js';

    let denomination = 'USD';
    let filter = 'all';

    let audusd = 0.67;
    let btcusd = 29516.78;

        

    function selectCurrency(event) {
        denomination = event.target.value;
    }

    function filterAssets(event) {
        filter = event.target.value;
    }
    
    function formatNumber(number) {
        return number.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }

    

    function calculateTotalValue(totalArg) {
        let totalValue = 0;
        
        if (totalArg === 'crypto' || filter == 'all') {
            data.crypto.forEach(item => {
                totalValue += item.amount * item.price;
            });
        }

        if (totalArg === 'stocks' || filter == 'all') {
            data.stocks.forEach(item => {
                totalValue += item.amount * item.price;
            });
        }

        if (totalArg === 'cash' || filter == 'all') {
            data.cash.forEach(item => {
                totalValue += item.amount * item.price;
            });
        }

        return totalValue;
  }
</script>

<style>

    .container {
        display: flex;
        flex-direction: column;
        height: 100vh;
    }

    .filter-container {
        display: flex;
        flex-direction: row;
        justify-content: center;
        margin-bottom: 20px;
    }

    h1, h2 {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        text-align: center;
    }

    select {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        font-size: 16px;
        margin: 10px;
        padding: 5px;
        width: fit-content;
        border-radius: 5px;
        background-color: #f5f5f5;
        color: #333;
    }

    select:hover {
        background-color: #97CAED;
        color: #fff;
    }

    table {
        border-collapse: collapse;
        width: 50%;
        margin-bottom: 20px;
        margin: auto
    }

    table, th, td {
        border: 1px solid #333;
    }

    th {
        background-color: #3498db;
        color: #333;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        font-weight: bold;
        padding: 10px;
        text-align: left;
        width: 25%;
    }

    td {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        padding: 8px;
    }

    td:hover {
        background-color: #5CFFB6;
    }

    tr:hover {
        background-color: #A5FFD6;
    }

</style>

<div class="container">
    <h1>Finances</h1>
    <div class="filter-container">
        <select id="currencyDropdown" on:change={selectCurrency}>
            <option value="USD">US Dollar</option>
            <option value="AUD">AU Dollar</option>
            <option value="BTC">Bitcoin</option>
        </select>
        <select id="filterDropdown"
                on:change={filterAssets}
                on:change={calculateTotalValue}
        >
            <option value="all">All</option>
            <option value="crypto">Crypto</option>
            <option value="stocks">Stocks</option>
            <option value="cash">Cash</option>
        </select>
    </div>
    <div>
        <h2>Assets</h2>
        <table>
            <thead>
                <tr>
                    <th>Ticker</th>
                    <th>Amount</th>

                    {#if denomination === 'USD'}
                    <th>Price ($USD)</th>
                    <th>Value ($USD)</th>

                    {:else if denomination === 'AUD'}
                    <th>Price ($AUD)</th>
                    <th>Value ($AUD)</th>

                    {:else if denomination === 'BTC'}
                    <th>Price (₿)</th>
                    <th>Value (₿)</th>
                    {/if}
                </tr>
            </thead>
            
            <!-- Display all crypto -->
            {#if filter == 'crypto' || filter == 'all'}
            <tbody>
                {#each data.crypto as item}
                <tr>
                    <td>{item.ticker}</td>
                    <td>{(item.amount)}</td>

                    {#if denomination === 'USD'}
                    <td>${formatNumber(item.price)}</td>
                    <td>${formatNumber(item.amount * item.price)}</td>

                    {:else if denomination === 'AUD'}
                    <td>${formatNumber(item.price / audusd)}</td>
                    <td>${formatNumber((item.amount * item.price) / audusd)}</td>

                    {:else if denomination === 'BTC'}
                    <td>₿{formatNumber(item.price / btcusd)}</td>
                    <td>₿{formatNumber((item.amount * item.price) / btcusd)}</td>
                    {/if}

                </tr>
                {/each}
            </tbody>
            {/if}

            <!-- Display all stocks -->
            {#if filter == 'stocks' || filter == 'all'}
            <tbody>
                {#each data.stocks as item}
                <tr>
                    <td>{item.ticker}</td>
                    <td>{item.amount}</td>

                    {#if denomination === 'USD'}
                    <td>${formatNumber(item.price)}</td>
                    <td>${formatNumber(item.amount * item.price)}</td>

                    {:else if denomination === 'AUD'}
                    <td>${formatNumber(item.price / audusd)}</td>
                    <td>${formatNumber((item.amount * item.price) / audusd)}</td>

                    {:else if denomination === 'BTC'}
                    <td>₿{formatNumber(item.price / btcusd)}</td>
                    <td>₿{formatNumber((item.amount * item.price) / btcusd)}</td>
                    {/if}
                </tr>
                {/each}
            </tbody>
            {/if}

            <!-- Display all cash -->
            {#if filter == 'cash' || filter == 'all'}
            <tbody>
                {#each data.cash as item}
                <tr>
                    <td>{item.ticker}</td>
                    <td>{item.amount}</td>

                    {#if denomination === 'USD'}
                    <td>${formatNumber(item.price)}</td>
                    <td>${formatNumber(item.amount * item.price)}</td>

                    {:else if denomination === 'AUD'}
                    <td>${formatNumber(item.price / audusd)}</td>
                    <td>${formatNumber((item.amount * item.price) / audusd)}</td>

                    {:else if denomination === 'BTC'}
                    <td>₿{formatNumber(item.price / btcusd)}</td>
                    <td>₿{formatNumber((item.amount * item.price) / btcusd)}</td>
                    {/if}
                </tr>
                {/each}
            </tbody>
            {/if}
            {#if filter == 'all'}
            <tfoot>
                <tr>
                    <td><strong>Total</strong></td>
                    <td></td>
                    <td></td>
                    {#if denomination === 'USD'}
                    <td><strong>${formatNumber(calculateTotalValue(filter))}</strong></td>

                    {:else if denomination === 'AUD'}
                    <td><strong>${formatNumber(calculateTotalValue(filter)/audusd)}</strong></td>

                    {:else if denomination === 'BTC'}
                    <td><strong>₿{formatNumber(calculateTotalValue(filter)/btcusd)}</strong></td>
                    {/if}

                </tr>
            </tfoot>
            {:else if filter == 'crypto'}
            <tfoot>
                <tr>
                    <td><strong>Total</strong></td>
                    <td></td>
                    <td></td>
                    {#if denomination === 'USD'}
                    <td><strong>${formatNumber(calculateTotalValue(filter))}</strong></td>

                    {:else if denomination === 'AUD'}
                    <td><strong>${formatNumber(calculateTotalValue(filter)/audusd)}</strong></td>

                    {:else if denomination === 'BTC'}
                    <td><strong>₿{formatNumber(calculateTotalValue(filter)/btcusd)}</strong></td>
                    {/if}                </tr>
            </tfoot>
            {:else if filter == 'stocks'}
            <tfoot>
                <tr>
                    <td><strong>Total</strong></td>
                    <td></td>
                    <td></td>
                    {#if denomination === 'USD'}
                    <td><strong>${formatNumber(calculateTotalValue(filter))}</strong></td>

                    {:else if denomination === 'AUD'}
                    <td><strong>${formatNumber(calculateTotalValue(filter)/audusd)}</strong></td>

                    {:else if denomination === 'BTC'}
                    <td><strong>₿{formatNumber(calculateTotalValue(filter)/btcusd)}</strong></td>
                    {/if}                </tr>
            </tfoot>
            {:else if filter == 'cash'}
            <tfoot>
                <tr>
                    <td><strong>Total</strong></td>
                    <td></td>
                    <td></td>
                    {#if denomination === 'USD'}
                    <td><strong>${formatNumber(calculateTotalValue(filter))}</strong></td>

                    {:else if denomination === 'AUD'}
                    <td><strong>${formatNumber(calculateTotalValue(filter)/audusd)}</strong></td>

                    {:else if denomination === 'BTC'}
                    <td><strong>₿{formatNumber(calculateTotalValue(filter)/btcusd)}</strong></td>
                    {/if}                </tr>
            </tfoot>
            {/if}
        </table>
    </div>
</div>
