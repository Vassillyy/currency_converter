<script>
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
                    <td class="tbMini"><button class="button">1</button></td>
                    <td class="tbMini"><button class="button">2</button></td>
                    <td class="tbMini"><button class="button">3</button></td>
                    <td class="tbMini"><button class="button">4</button></td>
                    <td class="tbMini"><button class="button">5</button></td>
                    <td class="tbMini"><button class="button del">del</button></td>
                </tr>

                <tr>
                    <td class="tbMini"><button class="button">6</button></td>
                    <td class="tbMini"><button class="button">7</button></td>
                    <td class="tbMini"><button class="button">8</button></td>
                    <td class="tbMini"><button class="button">9</button></td>
                    <td class="tbMini"><button class="button">0</button></td>
                    <td class="tbMini"><button class="button">.</button></td>
                </tr>
            {:else}
                <tr>
                    <td colspan="2"><button id="c" class="button">C</button></td
                    >
                    <td><button class="button mark">^</button></td>
                    <td><button class="button mark">/</button></td>
                </tr>

                <tr>
                    <td><button class="button">7</button></td>
                    <td><button class="button">8</button></td>
                    <td><button class="button">9</button></td>
                    <td><button class="button mark">*</button></td>
                </tr>

                <tr>
                    <td><button class="button">4</button></td>
                    <td><button class="button">5</button></td>
                    <td><button class="button">6</button></td>
                    <td><button class="button mark">-</button></td>
                </tr>

                <tr>
                    <td><button class="button">1</button></td>
                    <td><button class="button">2</button></td>
                    <td><button class="button">3</button></td>
                    <td><button class="button mark">+</button></td>
                </tr>

                <tr>
                    <td><button class="button">.</button></td>
                    <td><button class="button">0</button></td>
                    <td><button class="button del">del</button></td>
                    <td><button class="button mark">=</button></td>
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
        bottom: 150px;
        width: 600px;
        background-color: red;
        margin: 5vh auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        border-radius: 20px 20px 0 0;
        transition: height 1s;
        overflow: hidden;
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
    .button {
        width: 95%;
        height: 90%;
        font-weight: 600;
        font-style: italic;
        font-size: 30px;
        border-radius: 10px;
        border: 2px solid black;
    }
    button:active {
        transform: scale(0.95);
    }
    #changeSize {
        min-height: 10px;
        width: 40px;
        margin-bottom: 5px;
        background-color: LightSkyBlue;
        border-radius: 10px;
    }
    #c {
        background-color: LightSkyBlue;
        color: Gray;
    }
    .mark {
        background-color: Blue;
        color: white;
    }
    .del {
        color: Gray;
    }
    .tbMini {
        width: 100px;
        height: 50%;
        text-align: center;
    }
</style>
