<script lang="ts">
  import { NOUNS, ADJECTIVES } from "../data/lists";
  import { onMount } from "svelte";
  let names = new Array(20).fill("");
  let pinnedIndicies=[];

  const genOneName = () => {
    let adjective = ADJECTIVES[Math.floor(Math.random() * ADJECTIVES.length)];
    let noun = NOUNS[Math.floor(Math.random() * NOUNS.length)];
    return adjective + noun;
  };

  const handleGenerate = () => {
    // Reset the names array
    names=names.map((x,i)=>
      pinnedIndicies.indexOf(i)>-1?x:""
    )
    
    // Generate 20 new names
    
  };

  onMount(() => {
    window.setInterval(() => {
      names[names.indexOf("")] = genOneName();
    }, 1000 / 60);
  });

  const copy = (str) => {
    navigator.clipboard.writeText(str);
  };

  const pin = (name) => {
    const index=names.indexOf(name);
    if(pinnedIndicies.indexOf(index)>-1){
      pinnedIndicies=pinnedIndicies.filter(x=>x!==index);
    }else{
      pinnedIndicies.push(index);
    }
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
          copy(name);
        }}>📋</button
      >
      <span>{name}</span>
    </li>
  {/each}
</ul>
