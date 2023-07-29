<script lang="ts">
    // nested components
import Second from './Second.svelte';
import Nested from './Nested/+page.svelte'
import PackageInfo from './PackageInfo/+page.svelte'

    // dynamic attributes
    let name = 'Svelte'
    const src = "https://cdn.pixabay.com/photo/2016/08/08/09/17/avatar-1577909_1280.png"

    // HTML handling
    let string = 'This is a <strong>bold</strong> sentence'

    // assignment
    let count = 0
    
    // statements
    $: doubled = count * 2
    
    $: console.log(`the count is ${count}`)

    $: {
        console.log(`the count is ${count}`)
        console.log(`this will also be logged whenever count changes`)
    }

    $: if(count >=15){
        alert(`count is dangerously high!`)
        count = 0
    }

    function increment() {
        count += 1
    }

    // arrays and objects
    let numbers = [1,2,3,4,5]
    function addNumber(){
        // numbers.push(numbers.length + 1);
        // numbers = numbers
        numbers = [...numbers, numbers.length + 1]
    }

    function assignNumber(){
        numbers[numbers.length] = numbers.length + 1
    }

    const pkg = {
        name: 'svelte',
        speed: 'blaing',
        version: 4,
        website: 'https://svelte.dev'
    }
</script>

<h1>Hello {name.toUpperCase()}!</h1>
<!-- svelte-ignore a11y-img-redundant-alt -->
<img {src} alt="an image here">

<p>This is a paragraph.</p>
<Second />

<p>{@html string}</p>

<button on:click={increment}>
    Clicked {count}
    {count === 1 ? 'time' : 'times'}
</button>

<p>Doubled is {doubled}</p>

<button on:click={addNumber}>
    Add number to array
</button>

<button on:click={assignNumber}>
    Assign number to array
</button>
<ul>
    {#each numbers as num}
    <li>{num}</li>
    {/each}
</ul>

<Nested answer={'42'}/>
<Nested />

<!-- Spreading props -->
<PackageInfo {...pkg} />

{#if count > 10}
    <p>{count} is greater than 10</p>
    {:else}
    <p>{count} is betwee 0 and 10</p>
{/if}
<style>
    /* Styling */
    img {
        width: 100px;
    }

    p {
        color: goldenrod;
        font-family: 'Comic Sans MS', cursive;
        font-size: 2em;
    }

    ul {
        display: flex;
        justify-content: start;
        list-style: none;
        flex-wrap: wrap;
    }

    li {
        margin-inline: 2px;
    }
</style>