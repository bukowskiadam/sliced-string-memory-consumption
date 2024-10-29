<script lang="ts">
  import MemoryProblems from "./lib/MemoryProblems.svelte";
  import githubLogoBlack from "./assets/github-mark.svg";
  import githubLogoWhite from "./assets/github-mark-white.svg";
</script>

<main>
  <div class="card">
    <MemoryProblems />
  </div>
  <a
    href="https://github.com/bukowskiadam/sliced-string-memory-consumption"
    target="_blank"
    class="github-link"
  >
    <picture>
      <source srcset={githubLogoWhite} media="(prefers-color-scheme: dark)" />
      <source
        srcset={githubLogoBlack}
        media="(prefers-color-scheme: light), (prefers-color-scheme: no-preference)"
      />
      <img src={githubLogoBlack} alt="GitHub Logo" />
    </picture>
  </a>
</main>

<style>
  .github-link {
    position: absolute;
    top: 1rem;
    right: 1rem;
  }

  .github-link img {
    width: 32px;
    height: 32px;
  }
</style>
