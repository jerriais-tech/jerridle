<script context="module" lang="ts">
  import { words } from '../../utils';

	const pos = {
    '(n)': 'noun',
    '(v)': 'verb',
    '(adj)': 'adjective',
    '(pp)': 'past participle',
    '(adv)': 'adverb',
    '(int)': 'interjection',
    '(conj)': 'conjunction',
    '(interr)': 'interrogative',
    '(part)': 'participle',
    '(prep)': 'preposition',
    '(pron)': 'pronoun',
  };
</script>

<script lang="ts">
  export let word: string | undefined;
  export let definition: [string,string,string];
	/** The maximum number of alternate definitions to provide*/
	export let alternates = 9;

  $: {
    if (word && !definition) {
      definition = words.source[words.words.findIndex(w => word === w)];
    }
  };
</script>

<div class="def">
  {#if definition}
		<h2>{definition[0]}</h2>
		<em>{pos[definition[1]] || ''}</em>
		<ol>
			{#each definition[2].split(';') as def}
				<li>{def}</li>
			{/each}
		</ol>
  {/if}
</div>

<style>
	h2 {
		display: inline-block;
		margin-right: 1rem;
		margin-bottom: 0.8rem;
	}
	ol {
		padding-left: 1.5rem;
	}
	li {
		margin-bottom: 0.5rem;
	}
	li::marker {
		color: var(--fg-secondary);
	}
</style>
