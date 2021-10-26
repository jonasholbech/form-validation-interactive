<script>
  export let validateOn;
  export let clearOn;
  let eventsFired = [];
  let errorMessage = "";
  let successMessage = "";
  //when props change do stuff
  $: {
    console.log(validateOn, clearOn);
    errorMessage = "";
    successMessage = "";
  }

  const blur = (e) => {
    eventsFired = eventsFired.concat("blur");
    if (clearOn.includes("blur")) {
      errorMessage = "";
    }
    if (!validateOn.includes("blur")) {
      return;
    }
    validate(e);
  };
  const focus = (e) => {
    eventsFired = eventsFired.concat("focus");
    if (clearOn.includes("focus")) {
      errorMessage = "";
    }
    if (!validateOn.includes("focus")) {
      return;
    }
    validate(e);
  };
  const input = (e) => {
    eventsFired = eventsFired.concat("input");
    if (clearOn.includes("input")) {
      errorMessage = "";
    }
    if (!validateOn.includes("input")) {
      return;
    }
    validate(e);
  };
  const submit = (e) => {
    eventsFired = eventsFired.concat("submit");
    if (clearOn.includes("submit")) {
      errorMessage = "";
    }
    if (!validateOn.includes("submit")) {
      return;
    }
    validate({ target: e.target.querySelector("input") });
  };
  const validate = (e) => {
    if (e.target.checkValidity()) {
      successMessage = "Well done! Nice job!";
      errorMessage = "";
    } else {
      successMessage = "";
      errorMessage = "Hmm, there seems to be a problem with your input";
    }
  };
</script>

<form novalidate on:submit|preventDefault={submit}>
  <label>
    <h3>Add you e-mail, please</h3>
    <input
      type="email"
      required
      on:blur={blur}
      on:focus={focus}
      on:input={input}
    />
  </label>
  <p class="error">{errorMessage}</p>
  <p class="success">{successMessage}</p>

  <button type="submit">Submit</button>
</form>
<h3>Event log</h3>
<output><pre>{eventsFired.join("\n")}</pre></output>

<style>
  .error {
    color: red;
  }
  .success {
    color: green;
  }
  output {
    font-family: "Courier New", Courier, monospace;
  }
  pre {
    border: 1px solid #ccc;
    padding: 1rem;
  }
</style>
