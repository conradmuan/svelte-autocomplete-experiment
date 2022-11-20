<script>
  import { marked } from 'marked';

  let source = '';
  let mode = 'edit';
  let preview = marked(source);

  $: {
    preview = marked(source);
  }

  const handleClick = () => {
    mode = mode === 'preview' ? 'edit': 'preview';
  }
</script>

<main class="container">
  {#if mode === 'edit'}
    <button type="button" class="button" on:click={handleClick}>Preview</button>
    <textarea name="rawtext" id="rawtext" bind:value={source}></textarea>
  {/if}
  {#if mode === 'preview'}
    <button type="button" class="button" on:click={handleClick}>Edit</button>
    <div class="preview">{@html preview}</div>
  {/if}
</main>

<style>
  #rawtext {
    width: 100%;
    height: calc(100vh - 10vh);
    font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    font-size: 1.25rem;
  }
  .preview {
    height: calc(100vh - 10vh);
  }
  .container {
    width: 1080px;
  }
  .button {
    margin-bottom: 0.5rem;
  }
</style>
