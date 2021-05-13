<script>
    //Importing element from Svelte.js library
    import {setContext} from 'svelte';
    //Importing component to root file from component file
    import Navbar from './Navbar.svelte';
    import ExpenseData from './expenses';
    import ExpenseList from './ExpenseList.svelte';
    //setting up local variables to use data in root
    let expenses = [...ExpenseData]
    //functions to allow expenses to be deleted using JS
   function removeExpense(id) {
       expenses = expenses.filter(item => item.id !== id);
   }
   //Context
   setContext("remove", removeExpense);
</script>

<!--Rendering component to root component-->
<Navbar />
<main class="content">
    <ExpenseList {expenses} />
</main>
 