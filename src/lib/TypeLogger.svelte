<script>

  var generator = null;
  var baseText = 'In recent years, technology has enhanced the world of higher education, whether that world wanted it to or not. Given the wide availability of AI tools for both teachers and students though, more needs to be done to help a range of players in this industry navigate the challenges of technologically-enhanced teaching in the modern era.';
  var nextChar = null;
  var input = '';
  $: displayText = baseText.replace(input, `<span class="highlight">${input}</span>`)

  function handleKeydown(event) {
    event.preventDefault();

    if (event.key === 'Backspace') {
      // Do nothing.
      return
    }

    if (!generator) {
      // Start the sequence.
      generator = stringGenerator();
    }

    if (!nextChar) {
      // Get the next sequence value.
      nextChar = generator.next();
    }

    if (nextChar.done) {
      // Sequence is done. Well done!
      return
    }

    if (nextChar.value !== event.key) {
      // Pressed key is incorrect.
      return
    }

    // Key pressed is correct, update state.
    input += event.key
    nextChar = null;
  }

  function* stringGenerator() {
    for (const letter of baseText.split('')) {
      yield letter
    }
  }

</script>

<div>
  <h1>Practicar Touch Typing</h1>
</div>
<div id="text">
  <p>{@html displayText}</p>
</div>
<div id="input">
  <textarea bind:value={input} on:keydown={handleKeydown}></textarea>
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
    font-family: system-ui;
    margin-top: 1rem;
    background: white;
    border: 2px solid #3e4c40;
  }
  #input textarea {
    width: 100%;
    height: 35vh;
    border: none;
    outline: none;
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

