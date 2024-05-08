<script>
    import AddCurrency from "./AddCurrency.svelte";

    export let expression
    export let openList
    export let obj
    export let objUnder
    export let RemoveItemFromObjUnder
    export let  flagAnswer

    function handleKeydown(event) {
        if (!((event.key >= "0" && event.key <= "9") || event.key === ".")) {
            event.preventDefault();
        }
    }

</script>

<div class="container">
    <div class="selected">
        <button on:click={openList} class='flagCont'>
            <img src={obj.src} class="flag" alt="flag">
        </button>
        <div class="code">{obj.code}</div>
        <div class="name">{obj.name}</div>
        <img class="star"src="https://img.freepik.com/premium-vector/business-icon_518965-432.jpg?w=740" alt="star">
        <div class="numbers">
            <textarea maxlength='15' on:keydown={handleKeydown} bind:value={expression} placeholder="0"></textarea>
        </div>
    </div>
</div>

<AddCurrency {openList} {objUnder} {RemoveItemFromObjUnder} {obj} {expression} {flagAnswer} />

<style>
    .container {
        width: 600px;
        height: 70px;
        background-color: Lavender;
        margin: 0 auto;
        border-radius: 0 0 10px 10px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .selected {
        width: 580px;
        height: 50px;
        border-radius: 10px;
        background-color: white;
        position: relative;
    }
    .flagCont {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        background-color: red;
        padding: 0;
        position: absolute;
        top: 7%;
        left: 10px;
    }
    .flag {
        width: 100%;
        height: 100%;
        border-radius: 50%;
        border: 0.3px solid black;
    }
    .code {
        font-weight: 500;
        font-size: 20px;
        padding-left: 60px;
    }
    .name {
        color: gray;
        font-size: 14px;
        padding-left: 60px;
    }
    .star {
        width: 20px;
        height: 20px;
        position: absolute;
        top: 10px;
        right: 330px;
    }
    .numbers {
        width: 320px;
        height: 50px;
        position: absolute;
        right: 0;
        top: 0;
        border-radius: 0 10px 10px 0;
    }
    textarea {
        border-radius: 0 10px 10px 0;
        width: 100%;
        height: 100%;
        text-align: right;
        resize: none;
        border: none;
        outline: none;
        overflow: hidden;
        color: blue;
        font-size: 25px;
        font-weight: 700;
        letter-spacing: 5px;
    }
</style>
