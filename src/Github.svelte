<script>
    import {onMount} from "svelte";

    let users = [];
    let loading = true;

    onMount(async () => {
        let userData = await fetch('https://api.github.com/users');
        let githubUsers = await userData.json();

        users = githubUsers;
        loading = false;
    });
</script>

<h1>hello from github</h1>

{#if loading}
    <h2>loading...</h2>
{:else}
    <section>
    {#each users as user}
        <article class="user">
            <img src={user.avatar_url} alt={user.login}>
            <div class="user-info">
                <h3>User: {user.login}</h3>
                <a href={user.html_url} class="btn-primary" target="_blank">
                    Github URL
                </a>
            </div>
        </article>
    {/each}
    </section> 
{/if}