<script>
  let hue = 0;
  let cols = 10;
  let rows = 4;

  function generateHSL() {
    hue = (Math.random() * 360) | 0;
  }
</script>

<h1>Colour Theme</h1>

<button on:click={generateHSL}>Random Hue</button>
<p>Hue: {hue}</p>
<label for="hue">Hue:</label>
<input id="hue" type="range" min="0" max="360" step="1" bind:value={hue} />
<label for="rows">Rows:</label>
<input id="rows" type="range" min="0" max="100" step="1" bind:value={rows} />
<label for="cols">Columns:</label>
<input id="cols" type="range" min="0" max="100" step="1" bind:value={cols} />

{#each Array(rows)
  .fill()
  .map((_, i) => ++i) as row}
  <div class="row">
    {#each Array(cols)
      .fill()
      .map((_, i) => i) as col}
      <div
        class="box"
        style={`background-color: hsl(${hue},${(100 * col) / cols}%,${
          (100 * row) / rows
        }%)`}
      />
    {/each}
  </div>
{/each}

<style>
  button {
    cursor: pointer;
    padding: 5px;
    background-color: rgb(0, 100, 100);
    color: white;
    border: none;
    border-radius: 5px;
  }
  button:hover {
    background-color: rgb(0, 50, 50);
  }
  .row {
    display: flex;
  }
  .box {
    height: clamp(15px, 25px, 50px);
    width: clamp(15px, 25px, 50px);
    border: 1px solid black;
  }
</style>
