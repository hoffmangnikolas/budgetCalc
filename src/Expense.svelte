<script>
    export let id;
    export let name = "";
    export let amount = 0;
    export let removeExpense;
    let displayAmount = false;
    function toggleAmount (){
        displayAmount = !displayAmount;
    }
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>
            {name} <button class="amount-btn" on:click|once="{toggleAmount}">
                <i class="fas fa-caret-down" />
            </button>
        </h2>
        {#if displayAmount}
            <h4>amount : ${amount}</h4>
        {/if}
    </div>
    <div class="expense-button">
        <button class="expense-btn edit-btn">
            <i class="fas fa-pen"></i>
        </button>
        <button class="expense-btn delete-btn" on:click="{()=>removeExpense(id)}">
            <i class="fas fa-trash"></i>
        </button>
    </div>
</article>

