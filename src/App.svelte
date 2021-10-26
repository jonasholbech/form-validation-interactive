<script>
  import { SvelteToast } from "@zerodevx/svelte-toast";
  import Input1 from "./Input1.svelte";
  let validateOn = "blur";
  let clearOn = "focus";
  let validationOptions = ["blur", "focus", "input", "submit"];
</script>

<h1>The Awesome Form Event Playground</h1>
<main>
  <section>
    <h2>Clear Errors On</h2>
    {#each validationOptions as option, i (i)}
      <label
        ><input
          type="checkbox"
          name="clearOn"
          bind:group={clearOn}
          value={option}
        />
        {option}</label
      >
    {/each}
  </section>
  <section>
    <h2>Validate On</h2>
    {#each validationOptions as option, i (i)}
      <label
        ><input
          type="checkbox"
          name="validateOn"
          bind:group={validateOn}
          value={option}
        />
        {option}</label
      >
    {/each}
  </section>
  <hr />
  <Input1 {validateOn} {clearOn} />
</main>
<SvelteToast />

<style>
</style>
