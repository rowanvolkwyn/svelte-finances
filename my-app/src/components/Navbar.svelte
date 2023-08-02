<script>

</script>

<style>
    body {
        margin: 0 -10px;
        padding: 0;
        font-family: Arial, sans-serif;
    }

    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: #010026;
        height: 90px;
        padding: 10px 100px;
    }

    .logo img {
        width: 50px;
        height: 50px;
    }

    .links-container {
        flex-grow: 1;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .links {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .links a {
        color: #fff;
        text-decoration: none;
        margin: 0 20px;
        font-size: 18px;
        align-items: center;
    }

    .links a:hover {
        color: #97CAED;
        padding-bottom: 2px;
        transition: 500ms;
    }
</style>

<body>
    <nav class="navbar">
        <div class=links-container>
            <div class="links">
                <a href="#">Summary</a>
                <a href="#">Transactions</a>
                <a href="#">Rowan Volkwyn</a>
            </div>
        </div>
    </nav>
</body>