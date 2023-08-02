<script>

    import data from '../data.js';

    let denomination = 'USD';
    let filter = 'all';

    function selectCurrency(event) {
        denomination = event.target.value;
    }

    function filterAssets(event) {
        filter = event.target.value;
    }
    
    function formatNumber(number) {
        return number.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }

    

    function calculateTotalValue() {
        let totalValue = 0;
        
        if (filter === 'crypto' || filter == 'all') {
            data.crypto.forEach(item => {
                totalValue += item.amount * item.price;
            });
        }

        if (filter === 'stocks' || filter == 'all') {
            data.stocks.forEach(item => {
                totalValue += item.amount * item.price;
            });
        }

        if (filter === 'cash' || filter == 'all') {
            data.cash.forEach(item => {
                totalValue += item.amount * item.price;
            });
        }

        return totalValue;
  }
</script>

<style>

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

    /* Alternate row colors for better readability */
    tr:nth-child(even) {
        background-color: #f5f5f5;
    }

    tr:hover {
        background-color: #A5FFD6;
    }

    .table-container {
        margin: 0 auto;
        max-width: 800px;
    }

</style>

<div>
    <h1>Finances</h1>
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
    <div>
        <h2>Assets</h2>
        <table>
            <thead>
                <tr>
                    <th>Ticker</th>
                    <th>Amount</th>
                    <th>Price</th>
                    <th>Value</th>
                </tr>
            </thead>
            
            <!-- Display all crypto -->
            {#if filter == 'crypto' || filter == 'all'}
            <tbody>
                {#each data.crypto as item}
                <tr>
                    <td>{item.ticker}</td>
                    <td>{(item.amount)}</td>
                    <td>{formatNumber(item.price)}</td>
                    <td>{formatNumber(item.amount * item.price)}</td>
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
                    <td>{formatNumber(item.price)}</td>
                    <td>{formatNumber(item.amount * item.price)}</td>
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
                    <td>{formatNumber(item.price)}</td>
                    <td>{formatNumber(item.amount * item.price)}</td>
                </tr>
                {/each}
            </tbody>
            {/if}
            <tfoot>
                <tr>
                    <td><strong>Total</strong></td>
                    <td></td>
                    <td></td>
                    <td><strong>{formatNumber(calculateTotalValue())}</strong></td>
                </tr>
            </tfoot>
        </table>
    </div>
</div>
