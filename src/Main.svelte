<script>
  let user_input = '';
  let word_count = 0;
  let character_count = 0;
  let pos = [];
  let error = false;
  let count = 0;
  let star_word = "";

  const mode = (arr) => {
    return arr.sort((a,b) =>
          arr.filter(v => v===a).length - arr.filter(v => v===b).length
    ).pop();
  }

  const getOccurrence = (array, value) =>  {
    return array.filter((v) => (v === value)).length;

    }

  let wordpos = window.wordpos = new WordPOS({
    preload: true,
    // dictPath: 'https://unpkg.com/browse/wordpos-web@1.0.0/dict',
    dictPath: 'https://cdn.jsdelivr.net/npm/wordpos-web@1.0.2/dict',
    profile: true,
    debug: true,
    stopwords: false
  });

  const submit = (e) => {
    e.preventDefault()

      if (user_input == '') {
        error = true;
      }else{
        error = false
        let splits = user_input.split(" ")
        let add_up = splits.join('')
        character_count = add_up.length
        word_count = splits.length

   let words = wordpos.parse(user_input)
    star_word = mode(splits)

    count = getOccurrence(splits, star_word) + 1
 
  }
}
</script>

<div class="container">
<form on:submit = {submit}>
  <div class="bx--form-item">
    <label for="text-area-2" class="bx--label">Input</label>
    <div class="bx--form__helper-text">
      Enter you sentence or copy and paste your document here
    </div>
    <div class="bx--text-area__wrapper" data-invalid>
      <textarea bind:value="{user_input}" id="text-area-2" class="bx--text-area" rows="10" cols="400"></textarea>
    </div>
    {#if error}
      <div class="bx--form-requirement">Kindly provide a document to parse.</div>
    {/if}
  </div>

  <div class="bx--form-item">
    <button class="bx--btn bx--btn--primary" type="submit">Parse</button>
  </div>
</form>

<div class="bx--tile tile">
  <div class="bx--grid">
    <div class="bx--row">
      <div class="bx--col bx--col--auto box--col-sm-12">
        <h2>Word Count</h2>
        <h1>{word_count}</h1>
      </div>

      <div class="bx--col bx--col--auto box--col-sm-12">
        <h2>Character Count</h2>
        <h1>{character_count}</h1>
      </div>

      <div class="bx--col bx--col--auto box--col-sm-12">
        <h2>Star word</h2>
        <h3>{star_word}</h3>
        <p>appeared {count} times</p>
      </div>

    </div>
  </div>
</div>
</div>


<style>
  .container{
    margin: 5em;
  }
  .tile{
    margin-top: 1em;
    text-align: center;
  }
  .bx--btn{
    margin-top: 1em;
  }
  .cap{
    text-transform: capitalize;
  }
</style>