<script>
    import Calcul from "./calcul/Calcul.svelte";
    import List from "./listCarrency/List.svelte";
    import Header from "./header/Header.svelte";

    $: expression = '';

    function addToExpression(value) {
        if ('-+*/.'.includes(expression.at(-1)) && !isFinite(value)) {
            expression += '';
        }
        else if (expression === '' && !isFinite(value)) {
            expression += '';
        }
        else {
            expression += value;
        }
    }

    function clearInput() {
        expression = '';
    }

    function delChar() {
        expression = expression.slice(0, -1);
    }

    function calcul() {
        try {
            if (eval(expression) % 1 === 0) {
                expression = eval(expression).toString();
            }
            else if (eval(expression) % 0.1 === 0) {
                expression = eval(expression).toFixed(1).toString();
            }
            else {
                expression = eval(expression).toFixed(2).toString();
            }
        }
        catch(error) {
            expression = '';
        }
    }

    $: addList = false;

    function openList() {
        addList = true;
    }

    function closeList() {
        addList = false;
    }

    $: obj = {
        code: "RUB",
        name: "Российский Рубль",
        src: 'https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Flag_of_Russia.svg/1200px-Flag_of_Russia.svg.png'
    }

    function selectedItem(currency) {
        obj.code = currency.code;
        obj.name = currency.name;
        obj.src = currency.src;
        addList = false;
    }

    $: objUnder = []

    function selectedItemUnder(currency) {
        objUnder = [...objUnder, {code: currency.code, name: currency.name, src: currency.src}]
    }

    function RemoveItemFromObjUnder(currency) {
        objUnder = objUnder.filter(item => item.code !== currency.code);
        objUnder = objUnder;
    }

</script>

<div>
    {#if addList}
        <List {closeList} {obj} {selectedItem} {selectedItemUnder} {objUnder} {RemoveItemFromObjUnder}/>
    {:else}
        <Header {expression} {openList} {obj} {objUnder} {RemoveItemFromObjUnder} />
        <Calcul {calcul} {delChar} {clearInput} {addToExpression} />
    {/if}  
</div>

<style>
    div {
        width: 600px;
        display: flex;
        flex-direction: column;
        margin: 0 auto;
        position: relative;
        height: 700px;
    }
</style>
