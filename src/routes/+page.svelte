<script lang="ts">
  import { NOUNS, ADJECTIVES } from "../data/lists";
  import { onMount } from "svelte";
  let names = [];

  const genOneName = () => {
    let adjective = ADJECTIVES[Math.floor(Math.random() * ADJECTIVES.length)];
    let noun = NOUNS[Math.floor(Math.random() * NOUNS.length)];
    return adjective + noun;
  };

  const handleGenerate = () => {
    names = []; //new Array(20).fill(0).map(genOneName);
  };

  onMount(() => {
    window.setInterval(() => {
      if (names.length < 20) {
        names = [ ...names.slice(0, names.length),genOneName(),];
      }
    }, 1000/60);
  });

  const copy = (str) => {
    navigator.clipboard.writeText(str);
  };
</script>

<h1>Username Generator</h1>
<p>Generate your very own <a href="https://github.com/AlurienFlame">AlurienFlame</a>-style username!</p>
<button on:click={handleGenerate}>Regenerate</button>
<ul>
  {#each names as name}
    <li>
        <button
          on:click={() => {
            copy(name);
          }}>📋</button>
      <span>{name}</span>
    </li>
  {/each}
</ul>
