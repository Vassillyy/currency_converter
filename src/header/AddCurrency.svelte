<script>
    import { onMount } from 'svelte';

    export let openList
    export let obj
    export let objUnder
    export let RemoveItemFromObjUnder
    export let expression

    $: rates = [];

    async function addRetes() {
        const res = await fetch(`https://api.exchangerate-api.com/v4/latest/${obj.code}`);
        const data = await res.json();
        return rates = data.rates;
    }

    onMount(() => {
        addRetes();
        setInterval(() => {
            addRetes()
        }, 100000)
    })

    function formatLargeNumber(num) {
        let strNum = num.toFixed(2);
        let length = strNum.length;
        if (length <= 6) {
            return strNum;
        } else {
            let srartStr = strNum.slice(0, 5);
            let exponent = length - 5; 
            return `${srartStr} * 10^${exponent}`;
        }
    }
</script>

{#each objUnder as item (item.code)}
    {#if obj.code !== item.code}
    <div class="items">
        <div class="block">
            <img src={item.src} class="flag" alt="flag">
            <div class="code">{item.code}</div>
            <div class="name">{item.name}</div>
            {#await  addRetes()}
                <div class="text">Загрузка</div>
            {:then rates} 
                <div class="rate">1 {obj.code} = {rates[item.code]} {item.code}</div>
            {/await}
        </div>
        <div class="numbers">{formatLargeNumber(+expression * rates[item.code])}</div>
        <button on:click={RemoveItemFromObjUnder(item)} class="remove"><svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 94.926 94.926" style="enable-background:new 0 0 94.926 94.926;" xml:space="preserve"><g><path d="M55.931,47.463L94.306,9.09c0.826-0.827,0.826-2.167,0-2.994L88.833,0.62C88.436,0.224,87.896,0,87.335,0 c-0.562,0-1.101,0.224-1.498,0.62L47.463,38.994L9.089,0.62c-0.795-0.795-2.202-0.794-2.995,0L0.622,6.096 c-0.827,0.827-0.827,2.167,0,2.994l38.374,38.373L0.622,85.836c-0.827,0.827-0.827,2.167,0,2.994l5.473,5.476 c0.397,0.396,0.936,0.62,1.498,0.62s1.1-0.224,1.497-0.62l38.374-38.374l38.374,38.374c0.397,0.396,0.937,0.62,1.498,0.62 s1.101-0.224,1.498-0.62l5.473-5.476c0.826-0.827,0.826-2.167,0-2.994L55.931,47.463z"/></g></svg></button>
    </div>
    {/if}
{/each}
{#if objUnder.length < 10}
    <div class="container">
        <button on:click={openList} class="add"><svg id="Layer_1" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><linearGradient id="SVGID_1_" gradientUnits="userSpaceOnUse" x1="256" x2="256" y1="512" y2="0"><stop offset="0" stop-color="#5cc4bb"/><stop offset=".0968" stop-color="#50c1c0"/><stop offset=".5006" stop-color="#25b4d2"/><stop offset=".8152" stop-color="#0aacde"/><stop offset="1" stop-color="#00a9e2"/></linearGradient><path d="m256 0c-141.159 0-256 114.841-256 256s114.841 256 256 256 256-114.841 256-256-114.841-256-256-256zm0 480c-123.514 0-224-100.486-224-224s100.486-224 224-224 224 100.486 224 224-100.486 224-224 224zm155.199-224c0 8.837-7.163 16-16 16h-123.199v123.2c0 8.837-7.163 16-16 16s-16-7.163-16-16v-123.2h-123.201c-8.837 0-16-7.163-16-16 0-8.836 7.163-16 16-16h123.201v-123.199c0-8.836 7.163-16 16-16s16 7.164 16 16v123.199h123.199c8.837 0 16 7.164 16 16z" fill="url(#SVGID_1_)"/>
        </svg>Добавить котируемую валюту</button>
    </div>
{/if}

<style> 
    .container {
        width: 600px;
        height: 40px;
        margin: 5px auto;
        background-color: Lavender;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 10px;
        position: relative;
    }
    .add {
        width: 560px;
        height: 30px;
        border-radius: 10px;
        margin: 5px 10px;
        padding: 0;
        color: LightSkyBlue;
        border: 1px dashed black;
        background-color: white;
    }
    #Layer_1 {
        width: 20px;
        height: 20px;
        position: absolute;
        left: 160px;
        top: 10px;
    }
    .items {
        width: 600px;
        height: 40px;
        margin: 5px auto 0 auto;
        background-color: Lavender;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
    }
    .block {
        width: 430px;
        height: 30px;
        background-color: white;
        border-radius: 10px 0 0 10px;
        position: absolute;
        left: 20px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
    .flag {
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border: 0.3px solid black;
        margin-left: 10px;
    }
    .code {
        font-weight: 500;
        font-size: 20px;
        margin-left: 10px;
    }
    .name {
        color: gray;
        font-size: 14px;
        margin-left: 10px;
    }
    .rate {
        box-sizing: border-box;
        height: 100%;
        width: 120px ;
        margin: 0;
        padding: 10px 0;
        padding-right: 15px;
        position: absolute;
        right: 0;
        text-align: right;
        font-size: 10px;
        font-style: italic;
        color: CadetBlue;
        background-color: white;
    }
    .numbers {
        width: 120px;
        height: 30px;
        position: absolute;
        right: 20px;
        top: 5px;
        border-radius: 0 10px 10px 0;
        border-left: 2px solid Lavender;
        text-align: right;
        color: DarkSlateGray;
        font-weight: 500;
        font-size: 16px;
        padding-right: 15px;
        background-color: yellow;
    }
    #Capa_1 {
        width: 10px;
        height: 10px;
        position: absolute;
        right: 5px;
    } 
    .text {
        text-align: right;
        font-size: 10px;
        font-style: italic;
        color: CadetBlue;
        position: absolute;
        right: 0;
        margin-right: 10px;
    }
</style>