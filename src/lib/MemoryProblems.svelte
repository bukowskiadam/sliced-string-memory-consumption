<script lang="ts">
  const RANDOM_STRING_LENGTH = 5;
  const LONG_STRING_LENGTH = 1_000_000;
  // https://github.com/v8/v8/blob/e10e4796e63660e10c2b045a13e5439d63b3097f/src/objects/string.h#L940
  const MIN_SLICED_STRING_LENGTH = 13;

  let strings: string[] = [];

  $: str = strings.join("");
  $: count = strings.length;

  function makeRandomString(): string {
    return Math.random()
      .toString(36)
      .substring(2, 2 + RANDOM_STRING_LENGTH)
      .padEnd(RANDOM_STRING_LENGTH, "0");
  }

  function makeVeryLongRandomString(length: number): string {
    const result = [];
    for (let i = 0; i < length / RANDOM_STRING_LENGTH; i++) {
      result.push(makeRandomString());
    }
    return result.join("");
  }

  const addStrings = () => {
    const veryLongRandomString = makeVeryLongRandomString(LONG_STRING_LENGTH);
    const slicedString = veryLongRandomString.substring(
      0,
      MIN_SLICED_STRING_LENGTH
    );

    strings = [...strings, slicedString];
  };

  const addStrings10x = () => {
    for (let i = 0; i < 10; i++) {
      addStrings();
    }
  };
</script>

<div class="string-container">
  {str}
</div>

<p>&gt; {count} MB</p>
<p>
  <button on:click={addStrings}> Make me a memory problem! </button>
</p>
<p>
  <button on:click={addStrings10x}> Leaky pipe, memory spike! </button>
</p>

<style>
  .string-container {
    text-wrap: wrap;
    word-break: break-all;
    width: 500px;
    max-width: 80vw;
    min-height: 15em;
    margin: 2em auto;
    padding: 0.5em;
    border-radius: 1em;
    background-color: #1a1a1a;
    font-family: monospace;
    overflow: hidden;
  }

  @media (prefers-color-scheme: light) {
    .string-container {
      background-color: #f9f9f9;
    }
  }
</style>
