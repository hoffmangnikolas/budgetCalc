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
    let expenses = [...ExpenseData];
    //setting up editing variables
    let setName = "";
    let setAmount = null;
    let setId = null;

    //reactive from Svelte.js
    $: total = expenses.reduce((acc, curr)=>{
        return (acc += curr.amount);
    }, 0);

    //functions
   function removeExpense(id) {
       expenses = expenses.filter(item => item.id !== id);
   }
   function clearExpenses() {
       expenses = [];
   }
   function addExpense({name, amount}) {
       let expense = {id:Math.random() * Date.now(), name, amount};

       expenses = [expense,...expenses];
   }
   function setModifiedExpense(id) {
       let expense = expenses.find(item => item.id === id);

       setId = expense.id;
       setName = expense.name;
       setAmount = expense.amount;
   }

   //Context
   setContext("remove", removeExpense);
   setContext("modify", setModifiedExpense);
</script>

<!--Rendering component to root component-->
<Navbar />
<main class="content">
    <ExpenseForm {addExpense} />
    <Totals title="total expenses" {total} />
    <ExpenseList {expenses} />
    <button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>
        clear expenses
    </button>
</main>
 