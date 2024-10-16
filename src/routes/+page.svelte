<script lang="ts">
    import {NOUNS,ADJECTIVES} from "../data/lists"; 
let names = ["two", "three", "one"];

const genOneName = () => {
    let adjective=ADJECTIVES[Math.floor(Math.random() * ADJECTIVES.length)];
    let noun = NOUNS[Math.floor(Math.random() * NOUNS.length)];
    return adjective + noun;
}

const handleGenerate= ()=> {
    names = new Array(20).fill(0).map(genOneName);
}
</script>

<h1>Username Generator</h1>
<p>Generate your very own <a href="https://github.com/AlurienFlame">AlurienFlame</a>-style username!</p>
<button on:click={handleGenerate}
>Regenerate</button>
{#each names as names}
    <p>{names}</p>
{/each}