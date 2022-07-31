<script lang="ts">
    import openseaLogo from "../assets/opensea_logo_transparent.png";
    import Alchemy from "../Api/Alchemy";
    import {
        tokenAddressPunksComicOne,
        tokenAddressPunksComicOneSpecial,
        tokenAddressPunksComicTwo,
        tokenAddressFoundersDao,
        tokenAddressMintpass
    } from "../constants";

    export const floorPricesPunksComicOnePromise = Alchemy.nft.getFloorPrice(tokenAddressPunksComicOne);
    const floorPricesPunksComicOneSpecialPromise = Alchemy.nft.getFloorPrice(tokenAddressPunksComicOneSpecial);
    const floorPricesPunksComicTwoPromise = Alchemy.nft.getFloorPrice(tokenAddressPunksComicTwo);
    export const floorPricesFoundersDaoPromise = Alchemy.nft.getFloorPrice(tokenAddressFoundersDao);
    export const floorPricesMintpassOnePromise = Alchemy.nft.getFloorPrice(tokenAddressMintpass);
</script>

<div class="col pv-tile text-center">
    <h3 style="color: var(--pv-pink);">PUNKS Comic</h3>
    <p>Staked: <span id="staking-punks-comic">N/A</span> <span style="color: var(--pv-green);">(<span
            id="staking-punks-comic-percentage"></span>%)</span></p>
    <table class="table table-borderless pv-table" style="border-spacing: 28px;border-collapse: separate;">
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
                   href="https://opensea.io/collection/punks-comic?search[sortBy]=PRICE&search[sortAscending]=true&search[toggles][0]=BUY_NOW&search[stringTraits][0][name]=Type&search[stringTraits][0][values][0]=PUNKS%3A%20Issue%20%231"
                   class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                Punks Comic #1
            </td>
            {#await floorPricesPunksComicOnePromise}
                <td></td>
                <td></td>
            {:then floorPricesPunksComicOne}
                <td width="100">
                    {floorPricesPunksComicOne.openSea.floorPrice} Ξ
                </td>
                <td width="100">
                    {floorPricesPunksComicOne.looksRare.floorPrice} Ξ
                </td>
            {/await}
            <td>
                3313
            </td>
        </tr>
        <tr>
            <td>
                <a target="_blank"
                   href="https://opensea.io/collection/punks-comic?search[sortBy]=PRICE&search[sortAscending]=true&search[toggles][0]=BUY_NOW&search[stringTraits][0][name]=Type&search[stringTraits][0][values][0]=PUNKS%3A%20Issue%20%231%20%28Special%20Edition%29"
                   class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                Punks Comic #1 Special Edition
            </td>
            {#await floorPricesPunksComicOneSpecialPromise}
                <td></td>
                <td></td>
            {:then floorPricesPunksComicOneSpecial}
                <td width="100">
                    {floorPricesPunksComicOneSpecial.openSea.floorPrice} Ξ
                </td>
                <td width="100">
                    {floorPricesPunksComicOneSpecial.looksRare.floorPrice} Ξ
                </td>
            {/await}
            <td>
                58
            </td>
        </tr>
        <tr>
            <td>
                <a target="_blank"
                   href="https://opensea.io/collection/punks-comic?search[sortBy]=PRICE&search[sortAscending]=true&search[toggles][0]=BUY_NOW&search[stringTraits][0][name]=Type&search[stringTraits][0][values][0]=PUNKS%3A%20Issue%20%232"
                   class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                Punks Comic #2
            </td>
            {#await floorPricesPunksComicTwoPromise}
                <td></td>
                <td></td>
            {:then floorPricesPunksComicTwo}
                <td width="100">
                    {floorPricesPunksComicTwo.openSea.floorPrice} Ξ
                </td>
                <td width="100">
                    {floorPricesPunksComicTwo.looksRare.floorPrice} Ξ
                </td>
            {/await}
            <td>
                13566
            </td>
        </tr>
        <tr>
            <td>
                <a target="_blank"
                   href="https://opensea.io/collection/punks-comic?search[sortBy]=PRICE&search[sortAscending]=true&search[toggles][0]=BUY_NOW&search[stringTraits][0][name]=Type&search[stringTraits][0][values][0]=Pixel%20Vault%20Founder%27s%20DAO"
                   class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                Founders Dao
            </td>
            {#await floorPricesFoundersDaoPromise}
                <td></td>
                <td></td>
            {:then floorPricesFoundersDao}
                <td width="100">
                    {floorPricesFoundersDao.openSea.floorPrice} Ξ
                </td>
                <td width="100">
                    {floorPricesFoundersDao.looksRare.floorPrice} Ξ
                </td>
            {/await}
            <td>
                5902
            </td>
        </tr>
        <tr>
            <td>
                <a target="_blank"
                   href="https://opensea.io/collection/punks-comic?search[sortBy]=PRICE&search[sortAscending]=true&search[toggles][0]=BUY_NOW&search[stringTraits][0][name]=Type&search[stringTraits][0][values][0]=MintPass%20%231%3A%20MetaHero%20Identities"
                   class="opensea-link"><img src="{openseaLogo}" width="25"/></a>
                Mintpass #1: Metahero Identities
            </td>
            {#await floorPricesMintpassOnePromise}
                <td></td>
                <td></td>
            {:then floorPricesMintpassOne}
                <td width="100">
                    {floorPricesMintpassOne.openSea.floorPrice} Ξ
                </td>
                <td width="100">
                    {floorPricesMintpassOne.looksRare.floorPrice} Ξ
                </td>
            {/await}
            <td>
                <span id="supply-mintpass-one">3592</span>
            </td>
        </tr>
        </tbody>
    </table>
</div>