<script>
    import Calcul from "./calcul/Calcul.svelte";
    import List from "./listCarrency/List.svelte";
    import Header from "./header/Header.svelte";

    /** 
     * @type {string}
     * Переменная, которая хранит выражение в калькуляторе
    */
    $: expression = '';

    /**
     * @function
     * @param value - Значение для добавления к выражению.
     * Функция добавляет значение к выражению
     */
    function addToExpression(value) {
        if ('-+*/.'.includes(expression.at(-1)) && !isFinite(value)) {
            expression += '';
        }
        else if (expression === '' && !isFinite(value)) {
            expression += '';
        }
        else if (expression.includes('.') && value === '.') { 
            expression += '';
        }
        else {
            expression += value;
            flagAnswer = false;
        }
    }

    /**
     * @function
     * Функция удаляет содержимое выражения
     */
    function clearInput() {
        expression = '';
        flagAnswer = false;
    }

    /**
     * @function
     * Функция удаляет последний символ выражения
     */
    function delChar() {
        expression = expression.slice(0, -1);
        flagAnswer = false;
    }

    /**
     * @function
     * Функция подсчитывает выражение
     */
    function calcul() {
        try {
            if (eval(expression) % 1 === 0) {
                expression = eval(expression).toString();
                flagAnswer = true;
            }
            else if (eval(expression) % 0.1 === 0) {
                expression = eval(expression).toFixed(1).toString();
                flagAnswer = true;
            }
            else {
                expression = eval(expression).toFixed(2).toString();
                flagAnswer = true;
            }
        }
        catch(error) {
            expression = '';
            flagAnswer = false;
        }
    }

    /**
     * @type {boolean}
     * Переменная, указывающая открыт ли список валют или нет
     */
    $: addList = false;

    /**
     * @function
     * Функция открывающая список валют
     */
    function openList() {
        addList = true;
    }

    /**
     * @function
     * Функция закрывающая список валют
     */
    function closeList() {
        addList = false;
    }

     /**
     * @type {Object}
     * @property {string} code - Код валюты
     * @property {string} name - Название валюты
     * @property {string} src - Ссылка на изображение флага
     * Объект, который хранит данные базовой валюты (значение по умолчанию RUB)
     */
    $: obj = {
        code: "RUB",
        name: "Российский Рубль",
        src: 'https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Flag_of_Russia.svg/1200px-Flag_of_Russia.svg.png'
    }

    /**
     * @function
     * Функция которая меняет базовую валюту и закрывает список валют 
     */
    function selectedItem(currency) {
        obj.code = currency.code;
        obj.name = currency.name;
        obj.src = currency.src;
        addList = false;
    }

    /**
     * @type {Array}
     * Массив, который хранит данные котируемой валюты 
     */
    $: objUnder = []

    /**
     * @fun
     * @param currency - Валюта
     * Функция добавляет котируемую валюту в массив
     */
    function selectedItemUnder(currency) {
        objUnder = [...objUnder, {code: currency.code, name: currency.name, src: currency.src}]
    }

    /**
     * @function
     * @param currency - Валюта
     * Функция удаляет котируемую валюту из массива
     */
    function RemoveItemFromObjUnder(currency) {
        objUnder = objUnder.filter(item => item.code !== currency.code);
        objUnder = objUnder;
    }

    /**
     * @type {boolean}
     * Переменная, показывающая покажется ли подсчитанная котируемая валюта
     */
    $: flagAnswer = false
</script>

<div>
    {#if addList}
        <List {closeList} {obj} {selectedItem} {selectedItemUnder} {objUnder} {RemoveItemFromObjUnder}/>
    {:else}
        <Header {expression} {openList} {obj} {objUnder} {RemoveItemFromObjUnder} {flagAnswer}/>
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
