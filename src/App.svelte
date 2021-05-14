<script>
    //Importing element from Svelte.js library
    import {setContext} from 'svelte';
    //Importing component to root file from component file
    import Navbar from './Navbar.svelte';
    import ExpenseData from './expenses';
    import ExpenseList from './ExpenseList.svelte';
    import Totals from './Totals.svelte';
    import ExpenseForm from './ExpenseForm.svelte';
    //setting up local variables to use data in root
    let expenses = [...ExpenseData]
    //reactive from Svelte.js
    $: total = expenses.reduce((acc, curr)=>{
        return (acc += curr.amount)
    }, 0)
    //functions to allow expenses to be deleted using JS
   function removeExpense(id) {
       expenses = expenses.filter(item => item.id !== id);
   }
   function clearExpenses() {
       expenses=[];
   }
   //Context
   setContext("remove", removeExpense);
</script>

<!--Rendering component to root component-->
<Navbar />
<main class="content">
    <ExpenseForm />
    <Totals title="total expenses" {total} />
    <ExpenseList {expenses} />
    <button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>
        clear expenses
    </button>
</main>
 