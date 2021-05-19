<script>
    export let showForm;
</script>

<!-- HTML for Navbar-->
<nav class="nav">
    <div class="nav-center">
        <h1 class="nav-title">Budget Calculator</h1>
        <button type="button" class="nav-btn" on:click={showForm}>
            <i class="far fa-plus-square"/>
            add expense
        </button>
    </div>
</nav>