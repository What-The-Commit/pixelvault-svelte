<script lang="ts">
    import pixelvaultLogo from "./assets/pixelvault.png";
    import openseaLogo from "./assets/opensea_logo_transparent.png";
    import Currency from "./Components/Currency.svelte";
    import PunksComic from "./Components/PunksComic.svelte";

    async function getEthPriceInOtherCurrencies(currency = 'USD,EUR') {
        let response = await fetch("https://min-api.cryptocompare.com/data/price?fsym=ETH&tsyms=" + currency + "", {
            "headers": {
                "accept": "application/json"
            },
            "body": null,
            "method": "GET",
            "mode": "cors",
            "credentials": "omit"
        });

        let data = await response.json();

        return data;
    }

    let floorPricesPunksComicOnePromise;
    let floorPricesFoundersDaoPromise;
    let floorPricesMintpassOnePromise;

    $: if (floorPricesPunksComicOnePromise !== undefined && floorPricesFoundersDaoPromise !== undefined && floorPricesMintpassOnePromise !== undefined) {
        const genesisSet = Promise.all([floorPricesPunksComicOnePromise, floorPricesFoundersDaoPromise, floorPricesMintpassOnePromise]);
        genesisSet.then(function (all) {
            console.log(all)
        });
    }
</script>

<svelte:head>
    <link rel="icon" type="image/png" href="{pixelvaultLogo}"/>
</svelte:head>

<noscript>You need to enable JavaScript to run this app.</noscript>
<div class="cover-container d-flex w-100 h-100 p-3 mx-auto flex-column">
    <header class="mb-auto">
        <div>
            <h3 class="float-md-start mb-0"><img src="{pixelvaultLogo}" height="35">
                <div style="display: inline-block;position: relative;top: 4px;margin-left: 15px;color: var(--pv-pink);">
                    Pixel Vault
                </div>
            </h3>
            <nav class="nav nav-masthead justify-content-center float-md-end">
                <a class="nav-link active" aria-current="page" href="#">Home</a>
            </nav>
        </div>
    </header>

    <main>
        <div class="row tiles">
            {#await getEthPriceInOtherCurrencies()}
                Loading
            {:then ethPrices}
                <Currency currency="PUNKS" contract="0xa80ccc104349d2ee29998c54d6e6488012f8afe0" ethPriceInUsd="{ethPrices.USD}" />
                <Currency currency="POW" contract="0xc0793782d11dd9bf7b3a7a5a74614f1debe1da2e" ethPriceInUsd="{ethPrices.USD}" />
            {/await}
        </div>
        <h2 class="text-center"><b>Floor Prices</b></h2>
        <div class="row tiles">
            <PunksComic bind:floorPricesPunksComicOnePromise={floorPricesPunksComicOnePromise} bind:floorPricesFoundersDaoPromise={floorPricesFoundersDaoPromise} bind:floorPricesMintpassOnePromise={floorPricesMintpassOnePromise} />
            <div class="col pv-tile text-center">
                <h3 style="color: var(--pv-pink);">MetaHero Universe: Planet Tokens <a target="_blank"
                                                                                       href="https://opensea.io/collection/planetdaos"
                                                                                       class="opensea-link"><img
                        src="{openseaLogo}" width="25"/></a></h3>
                <table class="table table-borderless pv-table">
                    <thead style="color: var(--pv-green);">
                    <th></th>
                    <th>Floor price (OpenSea)</th>
                    <th>Floor price (LooksRare)</th>
                    <th>Supply</th>
                    </thead>
                    <tbody>
                    <tr>
                        <td>
                            Mercury
                        </td>
                        <td>
                            <span id="floor-planets-mercury"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-mercury"></span>
                        </td>
                        <td>
                            <span id="supply-planet-mercury">832</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Venus
                        </td>
                        <td>
                            <span id="floor-planets-venus"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-venus"></span>
                        </td>
                        <td>
                            <span id="supply-planet-venus">1438</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Earth
                        </td>
                        <td>
                            <span id="floor-planets-earth"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-earth"></span>
                        </td>
                        <td>
                            <span id="supply-planet-earth">1567</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Dark Moon
                        </td>
                        <td>
                            <span id="floor-planets-dark-moon"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-dark-moon"></span>
                        </td>
                        <td>
                            <span id="supply-planet-dark-moon">1567</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Mars
                        </td>
                        <td>
                            <span id="floor-planets-mars"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-mars"></span>
                        </td>
                        <td>
                            <span id="supply-planet-mars">1271</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Jupiter
                        </td>
                        <td>
                            <span id="floor-planets-jupiter"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-jupiter"></span>
                        </td>
                        <td>
                            <span id="supply-planet-jupiter">22602</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Saturn
                        </td>
                        <td>
                            <span id="floor-planets-saturn"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-saturn"></span>
                        </td>
                        <td>
                            <span id="supply-planet-saturn">4099</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Uranus
                        </td>
                        <td>
                            <span id="floor-planets-uranus"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-uranus"></span>
                        </td>
                        <td>
                            <span id="supply-planet-uranus">6122</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Neptune
                        </td>
                        <td>
                            <span id="floor-planets-neptune"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-neptune"></span>
                        </td>
                        <td>
                            <span id="supply-planet-neptune">6058</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Pluto
                        </td>
                        <td>
                            <span id="floor-planets-pluto"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-pluto"></span>
                        </td>
                        <td>
                            <span id="supply-planet-pluto">455</span>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Moon
                        </td>
                        <td>
                            <span id="floor-planets-moon"></span>
                        </td>
                        <td>
                            <span id="floor-lr-planets-moon"></span>
                        </td>
                        <td>
                            <span id="supply-planet-moon">710</span>
                        </td>
                    </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <h2 class="text-center"><b>Elite Apes Collector's Editions Floor Prices</b></h2>
        <div class="row tiles">
            <div class="col pv-tile text-center" style="border: none;">
                <table class="table table-borderless pv-table">
                    <thead style="color: var(--pv-green);">
                    <th></th>
                    <th>Floor price (OpenSea)</th>
                    <th>Floor price (LooksRare)</th>
                    <th>Supply</th>
                    </thead>
                    <tbody>
                    <tr>
                        <td style="width: 400px;">
                            <a target="_blank" href="https://opensea.io/collection/elite-ape-entry-coins"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape Entry Coins
                        </td>
                        <td>
                            <span id="floor-punks-comic-two-elite-ape-entry-coins"></span>
                        </td>
                        <td>
                            <span id="floor-lr-punks-comic-two-elite-ape-entry-coins"></span>
                        </td>
                        <td>
                            <span id="supply-punks-comic-two-elite-ape-entry-coins">17192</span>
                        </td>
                    </tr>
                    <tr>
                        <td style="width: 250px;">
                            <a target="_blank" href="https://opensea.io/collection/punks2biz" class="opensea-link"><img
                                    src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape Biz
                        </td>
                        <td>
                            <span id="floor-eliteape-biz"></span>
                        </td>
                        <td>
                            <span id="floor-lr-eliteape-biz"></span>
                        </td>
                        <td>
                            750
                        </td>
                    </tr>
                    <tr>
                        <td style="width: 250px;">
                            <a target="_blank" href="https://opensea.io/collection/punks2kingblackbored"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape King Black Bored
                        </td>
                        <td>
                            <span id="floor-eliteape-king-black-bored"></span>
                        </td>
                        <td>
                            <span id="floor-lr-eliteape-king-black-bored"></span>
                        </td>
                        <td>
                            750
                        </td>
                    </tr>
                    <tr>
                        <td style="width: 250px;">
                            <a target="_blank" href="https://opensea.io/collection/punks2bba" class="opensea-link"><img
                                    src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape BBA
                        </td>
                        <td>
                            <span id="floor-eliteape-bba"></span>
                        </td>
                        <td>
                            <span id="floor-lr-eliteape-bba"></span>
                        </td>
                        <td>
                            750
                        </td>
                    </tr>
                    <tr>
                        <td style="width: 250px;">
                            <a target="_blank" href="https://opensea.io/collection/punks2tropo"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape Tropo
                        </td>
                        <td>
                            <span id="floor-eliteape-tropo"></span>
                        </td>
                        <td>
                            <span id="floor-lr-eliteape-tropo"></span>
                        </td>
                        <td>
                            750
                        </td>
                    </tr>
                    <tr>
                        <td style="width: 250px;">
                            <a target="_blank" href="https://opensea.io/collection/punks2kiki" class="opensea-link"><img
                                    src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape Kiki
                        </td>
                        <td>
                            <span id="floor-eliteape-kiki"></span>
                        </td>
                        <td>
                            <span id="floor-lr-eliteape-kiki"></span>
                        </td>
                        <td>
                            750
                        </td>
                    </tr>
                    <tr>
                        <td style="width: 250px;">
                            <a target="_blank" href="https://opensea.io/collection/punks2gold-rilla"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape Goldrilla
                        </td>
                        <td>
                            <span id="floor-eliteape-gold-rilla"></span>
                        </td>
                        <td>
                            <span id="floor-lr-eliteape-gold-rilla"></span>
                        </td>
                        <td>
                            750
                        </td>
                    </tr>
                    <tr>
                        <td style="width: 250px;">
                            <a target="_blank" href="https://opensea.io/collection/punks2hanzo"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape Hanzo
                        </td>
                        <td>
                            <span id="floor-eliteape-hanzo"></span>
                        </td>
                        <td>
                            <span id="floor-lr-eliteape-hanzo"></span>
                        </td>
                        <td>
                            750
                        </td>
                    </tr>
                    <tr>
                        <td style="width: 250px;">
                            <a target="_blank" href="https://opensea.io/collection/punks2lone-star"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                            PUNKS 2: Elite Ape Lone Star
                        </td>
                        <td>
                            <span id="floor-eliteape-lone-star"></span>
                        </td>
                        <td>
                            <span id="floor-lr-eliteape-lone-star"></span>
                        </td>
                        <td>
                            750
                        </td>
                    </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <h2 class="text-center"><b>Sets Floor Prices</b></h2>
        <div class="row tiles">
            <div class="col pv-tile text-center">
                <h3 style="color: var(--pv-pink);">Genesis Set</h3>
                <b style="color: var(--pv-green);">PUNKS: Issue #1 + Pixel Vault Founder's DAO + MintPass #1 +
                    MetaHero</b>
                <p>
                    <b><span id="floor-set-genesis"></span></b>
                </p>
                <p>
                    <b><span id="floor-lr-set-genesis"></span></b>
                </p>
            </div>
            <div class="col pv-tile text-center">
                <h3 style="color: var(--pv-pink);">Planet Set</h3>
                <b style="color: var(--pv-green);">All 10 planets (except Dark Moon)</b>
                <p>
                    <b><span id="floor-set-planets"></span></b>
                </p>
                <p>
                    <b><span id="floor-lr-set-planets"></span></b>
                </p>
            </div>
        </div>

        <h2 class="text-center"><b>MetaHero Universe Floor Prices</b></h2>

        <div class="row tiles">
            <div class="col pv-tile text-center">
                <h3 style="color: var(--pv-pink);">Core Identities</h3>
                <table class="table table-borderless pv-table">
                    <thead style="color: var(--pv-green);">
                    <th></th>
                    <th>Floor price (OpenSea)</th>
                    <th>Floor price (LooksRare)</th>
                    <th>Supply</th>
                    </thead>
                    <tbody>
                    <tr>
                        <td width="185">
                            <a target="_blank"
                               href="https://opensea.io/collection/metaherouniverse?search[sortBy]=PRICE&search[sortAscending]=true&search[toggles][0]=BUY_NOW"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                            Overall
                        </td>
                        <td>
                            <span id="floor-metahero-core"></span>
                        </td>
                        <td>
                            <span id="floor-lr-metahero-core"></span>
                        </td>
                        <td>
                            <span id="supply-metahero-core">48</span>
                        </td>
                    </tr>
                    </tbody>
                </table>
            </div>
            <div class="col pv-tile text-center">
                <h3 style="color: var(--pv-pink);">Generative Identities</h3>
                <p>Staked: <span id="staking-metahero">N/A</span> <span style="color: var(--pv-green);">(<span
                        id="staking-metahero-percentage"></span>%)</span></p>
                <table class="table table-borderless pv-table">
                    <thead style="color: var(--pv-green);">
                    <th></th>
                    <th>Floor price (OpenSea)</th>
                    <th>Floor price (LooksRare)</th>
                    <th>Supply</th>
                    </thead>
                    <tbody>
                    <tr>
                        <td>
                            <a target="_blank"
                               href="https://opensea.io/collection/metahero-generative?search[sortAscending]=true&search[sortBy]=PRICE&search[toggles][0]=BUY_NOW"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                            Overall
                        </td>
                        <td>
                            <span id="floor-metahero"></span>
                        </td>
                        <td>
                            <span id="floor-lr-metahero"></span>
                        </td>
                        <td>
                            <span id="supply-metahero">6086</span>
                        </td>
                    </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <h2 class="text-center"><b>Collab Project Floor Prices</b></h2>
        <div class="row tiles">
            <div class="col pv-tile text-center">
                <h3 style="color: var(--pv-pink);">Collab Floor Prices</h3>
                <table class="table table-borderless pv-table">
                    <thead style="color: var(--pv-green);">
                    <th></th>
                    <th>Floor price (OpenSea)</th>
                    <th>Floor price (LooksRare)</th>
                    <th>Supply</th>
                    </thead>
                    <tbody>
                    <tr>
                        <td width="365">
                            <a target="_blank" href="https://opensea.io/collection/adidasoriginals"
                               class="opensea-link"><img src="{openseaLogo}" width="25"/></a>adidas
                            Originals: Into the Metaverse (Phase 1)
                        </td>
                        <td>
                            <span id="floor-collab-adidas"></span>
                        </td>
                        <td>
                            <span id="floor-lr-collab-adidas"></span>
                        </td>
                        <td>
                            <span id="supply-collab-adidas">30000</span>
                        </td>
                    </tr>
                    </tbody>
                </table>
            </div>

        </div>
    </main>

    <footer class="mt-auto text-white-50">
        <p style="float: left;">Made with ♥ by <a href="https://what-the-commit.com/" class="text-white">What The
            Commit</a> (<a
                href="https://twitter.com/bavragor94" class="text-white">tony-stark.eth</a>) for the <a
                href="https://punkscomic.com/" target="_blank" class="text-white">Pixel Vault</a> community

        </p>
        <!--<a href="#" id="fiat-button" onclick="toggleFiat(this)" style="float: right;">Show FIAT prices</a>-->
        <div class="clear"></div>
        <p>
            For supporting my projects and keep them running, feel free to tip <b
                style="color: white;">tony-stark.eth</b>
        </p>
    </footer>
</div>