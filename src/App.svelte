<script>
    //Importing element from Svelte.js library
    import {setContext, onMount, afterUpdate} from 'svelte';
    //Importing prop/component to root file from component file
    import Navbar from './Navbar.svelte';
    import ExpenseList from './ExpenseList.svelte';
    import Totals from './Totals.svelte';
    import ExpenseForm from './ExpenseForm.svelte';
    //import ExpenseData from './expenses';
    
    //setting up local variable to use data the user input
    let expenses = [];
    //setting up editing variables
    let setName = "";
    let setAmount = null;
    let setId = null;
    //setting up toggle form varibles
    let isFormOpen = false;

    //reactive from Svelte.js
    $: isEditing = setId?true:false;
    $: total = expenses.reduce((acc, curr)=>{
        return (acc += curr.amount);
    }, 0);

    //functions
    function showForm() {
        isFormOpen = true;
    }

    function hideForm() {
        isFormOpen = false;
        setName = '';
        setAmount = null;
        setId = null;
    }

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
       showForm();
   }
    function editExpense({name, amount}) {
        expenses = expenses.map(item => {
            return item.id === setId? {...item, name, amount}:{...item};
        });
        setId = null;
        setAmount = null;
        setName = "";
    }

   //Context
   setContext("remove", removeExpense);
   setContext("modify", setModifiedExpense);

   //Local storage
    function setLocalStorage() {
        localStorage.setItem("expenses", JSON.stringify(expenses));
    }
    //lifecycle functions used to grab items from local storage
    onMount(() => {
        expenses = localStorage.getItem("expenses")
        ? JSON.parse(localStorage.getItem("expenses")):[];
    });
    afterUpdate(() => {
        console.log("after update");
        setLocalStorage();
    });

</script>

<!--Rendering component to root component-->
<Navbar {showForm} />
<main class="content">
    {#if isFormOpen}
        <ExpenseForm 
            {addExpense} 
            name={setName} 
            amount={setAmount} 
            {isEditing} 
            {editExpense}
            {hideForm} 
        />
    {/if}
    <Totals title="total expenses" {total} />
    <ExpenseList {expenses} />
    <button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>
        clear expenses
    </button>
</main>
 