<script lang="ts">
    export let ethPriceInUsd: number;
    export let currency: string;
    export let contract: string;

    async function fetchPriceInWeth(pool: string) {
        let response = await fetch("https://api.thegraph.com/subgraphs/name/uniswap/uniswap-v3", {
            "body": "{\"query\":\"\\n  {\\n    pool(id: \\\"" + pool + "\\\") {\\n      token1Price\\n    }\\n  }\\n\"}",
            "method": "POST",
            "mode": "cors",
            "credentials": "omit"
        });

        let data = await response.json();

        return data.data.pool.token1Price;
    }

    async function addTokenToMetamask() {
        if (ethereum === undefined) {
            console.error('no wallet');
            return;
        }

        try {
            // wasAdded is a boolean. Like any RPC method, an error may be thrown.
            await ethereum.request({
                method: 'wallet_watchAsset',
                params: {
                    type: 'ERC20', // Initially only supports ERC20, but eventually more!
                    options: {
                        address: contract, // The address that the token is at.
                        symbol: currency.toUpperCase(), // A ticker symbol or shorthand, up to 5 chars.
                        decimals: 18, // The number of decimals in the token
                    },
                },
            });
        } catch (error) {
            console.error(error);
        }
    }
</script>

<div class="col pv-tile text-center">
    <p>
        <b>${currency.toUpperCase()} Price</b><br/>
        <b style="color: var(--pv-green);" id="token-price-{currency.toLowerCase()}">
            {#await fetchPriceInWeth(contract)}N/A{:then priceInWeth}{(priceInWeth * ethPriceInUsd).toFixed(3).toLocaleString()}{/await}
        </b>
    </p>
    <p>
        <a href="https://www.dextools.io/app/ether/pair-explorer/{contract}"
           class="link-light" target="_blank"><b>Dextools</b></a>
    </p>
    <p>
        <a href="#" class="link-light" on:click={addTokenToMetamask}><b>Add to
            Metamask</b></a>
    </p>
</div>