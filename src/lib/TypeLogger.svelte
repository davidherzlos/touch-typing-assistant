<script>

  var baseText = `In recent years, technology has enhanced the world of higher education, 
                  whether that world wanted it to or not. Given the wide availability of
                  AI tools for both teachers and students though, more needs to be done to help.`;
  var typed = '';
  const strGenerator = stringGenerator();
  var next = null;

  function* stringGenerator() {
    for (const letter of baseText.split('')) {
      yield letter
    }
  }

  function handleKeydown(event) {
    event.preventDefault();
    if (!next) {
      next = strGenerator.next();
    }
    if (!next.done && next.value === event.key) {
      typed += event.key;
      next = null;
    }
  }

  $: displayText = baseText.replace(typed, `<span class="highlight">${typed}</span>`)

</script>

<div>
  <h1>Practicar Touch Typing</h1>
</div>
<div id="text">
  <p>{@html displayText}</p>
</div>
<div id="input">
  <textarea bind:value={typed} on:keydown={handleKeydown}></textarea>
</div>

<style>
  :global(.highlight) {
    font-weight: bold;
    color: green;
  }
  #text, #input {
    border: 2px solid #a3c5a6;
    padding: 1rem;
    border-radius: 10px;
  }
  #text {
    background: #e4f1e5;
  }
  #input {
    margin-top: 1rem;
    background: white;
    border: 2px solid #3e4c40;
  }
  #input textarea {
    width: 100%;
    height: 35vh;
    border: none;
    outline: none;
    font-family: system-ui;
  }
  @media (prefers-color-scheme: dark) {
    #text, #input {
      border: 2px solid #2e2e60;
    }
    #text, #input {
      background: #1f1f2a;
    }
    #text {
      background: #1f1f2a;
    }
    #input {
      margin-top: 1rem;
      background: #1f1f2a;
      border: 2px solid #3e4c40;
    }
    #input textarea {
      width: 100%;
      height: 35vh;
      border: none;
      outline: none;
      background: #1f1f2a;
    }
  }
</style>
