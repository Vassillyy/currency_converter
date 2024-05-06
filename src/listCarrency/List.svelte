<script>
    import { currencies } from "./currency.js";

    currencies.sort((a, b) => a.code.localeCompare(b.code));

    let str = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    export let closeList
    export let selectedItem
    export let obj
    export let selectedItemUnder

</script>

<div class="container">
    <div class="miniContainer">
        <button on:click={closeList} id="closeList"
            ><svg class="arrow" viewbox="0 0 60 100"
                ><path
                    d="M 50,0 L 60,10 L 20,50 L 60,90 L 50,100 L 0,50 Z"
                /></svg
            ></button>
        <h1>Валюты</h1>
        
    </div>
    <table>
        {#each str as char}
            {#if currencies.some((currency) => currency.code.startsWith(char))}
                <div class="char">{char}</div>
                {#each currencies as currency (currency.code)}
                    {#if currency.code.startsWith(char)}
                        <tr >
                            <td>
                                <button on:click={() => selectedItem(currency)} class="buttonFlag">
                                    <img src={currency.src} alt="flag" class="img"/>
                                </button>
                                <div class="code">{currency.code}</div>
                                <div class="name">{currency.name}</div>
                                {#if currency.code === obj.code}
                                    <p>Базовая валюта</p>
                                    <img class="star"src="https://img.freepik.com/premium-vector/business-icon_518965-432.jpg?w=740" alt="star">
                                {:else}
                                    <button on:click={() => selectedItemUnder(currency)} class="add"><svg class='arrowMin' version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 975.9 975.9" style="enable-background:new 0 0 975.9 975.9;" xml:space="preserve"><g><path d="M386.842,940.801c23.4,23.399,54.101,35.1,84.9,35.1s61.4-11.7,84.9-35.1l368-368l0,0c19.6-19.601,33.199-47.601,35-75.4 c0.5-7.9,0.5-16.5-0.7-24.3c-2.2-15-6.5-29.601-13.9-42.9c-5.5-9.899-12.399-19.1-20.399-27.1l0,0l-368-368 c-46.9-46.801-122.9-46.801-169.801,0c-46.899,46.899-46.899,122.8,0,169.699L549.942,367.9h-414c-66.3,0-120,53.7-120,120 s53.7,120,120,120h414l-163.101,163.2C339.942,818,339.942,894,386.842,940.801z"/></g>
                                    </svg>в котируемую валюту</button>
                                {/if}
                            </td>
                        </tr>
                    {/if}
                {/each}
            {/if}
        {/each}
    </table>
</div>

<style>
    .container {
        width: 600px;
        margin: 0 auto;
        padding-bottom: 40px;
    }
    .miniContainer {
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        align-items: center;
    }
    #closeList {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 0;
        border: 0;
        background-color: white;
    }
    .arrow {
        border-radius: 50%;
        width: 40px;
        height: 40px;
        cursor: pointer;
        cursor: pointer;
    }
    .arrow path {
        fill: Silver;
        stroke-width: 4;
        stroke: #759bbc;
        transition: fill 0.5s ease-out;
    }
    .arrow:hover path {
        fill: black;
    }
    h1 {
        margin-left: 15px;
    }
    table {
        width: 100%;
        border-collapse: collapse;
    }
    .char {
        color: gray;
        font-weight: 500;
        font-size: 17px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    tr {
        margin: 0;
        height: 50px;
        position: relative;
    }
    td {
        border: 1px solid grey;
    }
    .buttonFlag {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        position: absolute;
        padding: 0;
        margin-left: 10px;
        top: 10%;
    }
    .img {
        width: 100%;
        height: 100%;
        border-radius: 50%;
        border: 0.3px solid black;
    } 
    .code {
        font-weight: 500;
        font-size: 15px;
        padding-left: 80px;
    }
    .name {
        color: gray;
        font-size: 13px;
        padding-left: 80px;
    }
    .star {
        width: 20px;
        height: 20px;
        position: absolute;
        top: 15px;
        right: 30px;
    }
    p {
        position: absolute;
        right: 70px;
        top: 10px;
        margin: 0;
        color: grey;
        font-size: 20px;
    }
    .add {
        position: absolute;
        right: 10px;
        top: 10px;
        font-size: 15px;
        height: 30px;
        border: none;
        background-color: white;
        color: LightGray;
    }
    .arrowMin {
        width: 20px;
        height: 20px;
        position: absolute;
        right: 160px;
    }
    .arrowMin path {
        fill: LightGray;
    }
</style>
