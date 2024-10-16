<script lang="ts">
  import { NOUNS, ADJECTIVES } from "../data/lists";
  import { onMount } from "svelte";
  let names = new Array(20).fill("").map((text) => ({ text, pinned: false }));

  const genName = () => {
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
      let firstEmpty = names.findIndex(({ text }) => text === "");
      if (firstEmpty >= 0) names[firstEmpty].text = genName();
    }, 1000 / 60);
  });

  const copy = (str) => {
    navigator.clipboard.writeText(str);
  };

  const pin = (name) => {
    name.pinned = !name.pinned;
    names = names; // refresh
  };
</script>

<main>
  <h1>Username Generator</h1>
  <p>Generate your very own <a href="https://github.com/AlurienFlame">AlurienFlame</a>-style username!</p>
  <button on:click={handleGenerate} class="regen-button">Regenerate</button>
  <ul>
    {#each names as name}
      <li>
        <button
          class="action-button"
          on:click={() => {
            pin(name);
          }}
          ><span class="material-symbols-outlined">
            keep{name.pinned ? "" : "_off"}
          </span>
        </button>
        <button
          on:click={() => {
            copy(name.text);
          }}
          class="action-button"><span class="material-symbols-outlined"> content_copy </span></button
        >
        <span class:pinned-text={name.pinned}>{name.text}</span>
      </li>
    {/each}
  </ul>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    max-width: 60ch;
    margin: 0px auto;
    align-items: center;
  }
  button {
    background: #dd6f7a;
    border: none;
    cursor: pointer;
    color: white;
    border-radius: 0.5rem;
    &:hover {
      filter: brightness(0.9);
    }
    &:active {
      filter: brightness(0.8);
    }
  }
  .regen-button {
    padding: 0.5rem 1rem;
  }
  .action-button {
    width: 32px;
    height: 32px;
    align-items: center;
  }
  ul {
    list-style-type: none;
    gap: 0.25rem;
    display: flex;
    flex-direction: column;
  }
  .pinned {
    filter: brightness(0.7);
  }
  a {
    color: #5e81ac;
  }
  a:visited {
    color: #5e81ac;
  }
</style>
