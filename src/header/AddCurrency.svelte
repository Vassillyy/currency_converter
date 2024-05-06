<script>
    export let openList
    export let objUnder
</script>


{#each objUnder as item (item.code)}
    <div class="items">
        <div class="block">
            <img src={item.src} class="flag" alt="flag">
            <div class="code">{item.code}</div>
            <div class="name">{item.name}</div>
        </div>
        <div class="numbers">
            <textarea maxlength="15"></textarea>
        </div>
    </div>
{/each}
<div class="container">
    <button on:click={openList} class="add"><svg id="Layer_1" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><linearGradient id="SVGID_1_" gradientUnits="userSpaceOnUse" x1="256" x2="256" y1="512" y2="0"><stop offset="0" stop-color="#5cc4bb"/><stop offset=".0968" stop-color="#50c1c0"/><stop offset=".5006" stop-color="#25b4d2"/><stop offset=".8152" stop-color="#0aacde"/><stop offset="1" stop-color="#00a9e2"/></linearGradient><path d="m256 0c-141.159 0-256 114.841-256 256s114.841 256 256 256 256-114.841 256-256-114.841-256-256-256zm0 480c-123.514 0-224-100.486-224-224s100.486-224 224-224 224 100.486 224 224-100.486 224-224 224zm155.199-224c0 8.837-7.163 16-16 16h-123.199v123.2c0 8.837-7.163 16-16 16s-16-7.163-16-16v-123.2h-123.201c-8.837 0-16-7.163-16-16 0-8.836 7.163-16 16-16h123.201v-123.199c0-8.836 7.163-16 16-16s16 7.164 16 16v123.199h123.199c8.837 0 16 7.164 16 16z" fill="url(#SVGID_1_)"/>
    </svg>Добавить котируемую валюту</button>
</div>


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
        width: 580px;
        height: 30px;
        border-radius: 10px;
        margin: 5px 10px;
        padding: 0;
        color: LightSkyBlue;
        border: 1px dashed black;
        background-color: white;
    }
    svg {
        width: 20px;
        height: 20px;
        position: absolute;
        left: 160px;
        top: 10px;
    }
    .items {
        width: 600px;
        height: 40px;
        margin: 5px auto;
        background-color: Lavender;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
    }
    .block {
        width: 350px;
        height: 30px;
        background-color: white;
        border-radius: 10px 0 0 10px;
        position: absolute;
        left: 10px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
    .flag {
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border: 0.3px solid black;
        margin-left: 15px;
    }
    .code {
        font-weight: 500;
        font-size: 20px;
        margin-left: 15px;
    }
    .name {
        color: gray;
        font-size: 14px;
        margin-left: 15px;
    }
    .numbers {
        width: 250px;
        height: 30px;
        position: absolute;
        right: 10px;
        top: 5px;
        border-radius: 0 10px 10px 0;
    }
    textarea {
        width: 100%;
        height: 30px;
        text-align: right;
        resize: none;
        border: none;
        outline: none;
        overflow: hidden;
        font-size: 20px;
        font-weight: 500;
        letter-spacing: 5px;
        border-radius: 0 10px 10px 0;
        color: DodgerBlue;
    }
</style>