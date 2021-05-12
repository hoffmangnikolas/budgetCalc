<script>
    //components
    import SectionTitle from './Title.svelte';
    import Expense from './Expense.svelte';
    //variables
    export let expenses = [];
    export let removeExpense;
</script>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>

<section>
    <SectionTitle title="expense list" />
    <ul>
        {#each expenses as expense, index}
            <Expense {...expense} {removeExpense} />
            {:else}
            <h2>currently you have no expenses</h2>
        {/each}
    </ul>
</section>