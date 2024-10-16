<script lang="ts">
  import { NOUNS, ADJECTIVES } from "../data/lists";
  import { onMount } from "svelte";
  let names = new Array(20).fill("").map(text=>({text,pinned:false}));

  const genOneName = () => {
    let adjective = ADJECTIVES[Math.floor(Math.random() * ADJECTIVES.length)];
    let noun = NOUNS[Math.floor(Math.random() * NOUNS.length)];
    return adjective + noun;
  };

  const handleGenerate = () => {
    // Reset the unpinned names in array
    names.forEach((name) => {
      if (!name.pinned) {
        name.text = "";
      }
    });
  };

  onMount(() => {
    window.setInterval(() => {
      names[names.findIndex(({text})=>text==="")].text = genOneName();
    }, 1000 / 60);
  });

  const copy = (str) => {
    navigator.clipboard.writeText(str);
  };

  const pin = (name) => {
    name.pinned = !name.pinned;
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
          pin(name);
        }}>📍</button
      >
      <button
        on:click={() => {
          copy(name.text);
        }}>📋</button
      >
      <span>{name.text}</span>
    </li>
  {/each}
</ul>
