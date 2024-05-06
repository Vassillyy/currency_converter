<script>
    export let addToExpression
    export let clearInput
    export let delChar
    export let calcul

    $: height = 410;

    function change() {
        if (height === 410) {
            height -= 310;
        } else height += 310;
    }
</script>

<div class="container" style="height: {height}px">
    <button id="changeSize" on:click={change}></button>
    <table>
        <tbody>
            {#if height === 100}
                <tr>
                    <td class="tbMini"><button on:click={() => addToExpression(1)} class="buttonMin">1</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression(2)} class="buttonMin">2</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression(3)} class="buttonMin">3</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression(4)} class="buttonMin">4</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression(5)} class="buttonMin">5</button></td>
                    <td class="tbMini"><button on:click={delChar} class="buttonMin del">del</button></td>
                </tr>

                <tr>
                    <td class="tbMini"><button on:click={() => addToExpression(6)} class="buttonMin">6</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression(7)} class="buttonMin">7</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression(8)} class="buttonMin">8</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression(9)} class="buttonMin">9</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression(0)} class="buttonMin">0</button></td>
                    <td class="tbMini"><button on:click={() => addToExpression('.')} class="buttonMin">.</button></td>
                </tr>
            {:else}
                <tr>
                    <td colspan="2"><button on:click={clearInput} id="c" class="button">C</button></td
                    >
                    <td><button on:click={() => addToExpression('**')} class="button mark">^</button></td>
                    <td><button on:click={() => addToExpression('/')} class="button mark">/</button></td>
                </tr>

                <tr>
                    <td><button on:click={() => addToExpression(7)} class="button">7</button></td>
                    <td><button on:click={() => addToExpression(8)} class="button">8</button></td>
                    <td><button on:click={() => addToExpression(9)} class="button">9</button></td>
                    <td><button on:click={() => addToExpression('*')} class="button mark">*</button></td>
                </tr>

                <tr>
                    <td><button on:click={() => addToExpression(4)} class="button">4</button></td>
                    <td><button on:click={() => addToExpression(5)} class="button">5</button></td>
                    <td><button on:click={() => addToExpression(6)} class="button">6</button></td>
                    <td><button on:click={() => addToExpression('-')} class="button mark">-</button></td>
                </tr>

                <tr>
                    <td><button on:click={() => addToExpression(1)} class="button">1</button></td>
                    <td><button on:click={() => addToExpression(2)} class="button">2</button></td>
                    <td><button on:click={() => addToExpression(3)} class="button">3</button></td>
                    <td><button on:click={() => addToExpression('+')} class="button mark">+</button></td>
                </tr>

                <tr>
                    <td><button on:click={() => addToExpression('.')} class="button">.</button></td>
                    <td><button on:click={() => addToExpression(0)} class="button">0</button></td>
                    <td><button on:click={delChar} class="button del">del</button></td>
                    <td><button on:click={calcul} class="button mark">=</button></td>
                </tr>
            {/if}
        </tbody>
    </table>
</div>


<style>
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }
    .container {
        position: absolute;
        bottom: 0;
        width: 600px;
        background-color: Lavender;
        margin: 5vh auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        border-radius: 20px 20px 0 0;
        transition: height 1s;
        overflow: hidden;
    }
    #changeSize {
        min-height: 10px;
        width: 40px;
        margin-bottom: 5px;
        background-color: LightSkyBlue;
        border-radius: 10px;
    }
    table {
        border-collapse: collapse;
        width: 100%;
        height: 400px;
    }
    td {
        text-align: center;
        width: 25%;
        height: 20%;
    }
    .tbMini {
        width: 100px;
        height: 50%;
        text-align: center;
    }
    .buttonMin {
        width: 95%;
        height: 80%;
        font-weight: 600;
        font-style: italic;
        font-size: 25px;
        border-radius: 10px;
        border: 2px solid black;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 auto;
    }
    .button {
        width: 95%;
        height: 90%;
        font-weight: 600;
        font-style: italic;
        font-size: 30px;
        border-radius: 10px;
        border: 2px solid black;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 auto;
    }
    button:active {
        transform: scale(0.95);
    }
    .mark {
        background-color: Blue;
        color: white;
    }
    #c {
        background-color: LightSkyBlue;
        color: Gray;
    }
    .del {
        color: Gray;
    }
</style>
