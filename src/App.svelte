<script>
  import Timer from './Timer.svelte';
  import HowTo from './HowTo.svelte';

  let audio;

  const handleTimerEnd = () => {
    audio.play();
  };
</script>

<style>
  h1 {
    text-align: center;
  }
</style>

<h1>Handwashing App</h1>
<Timer on:end={handleTimerEnd} />
<HowTo />

<!-- svelte-ignore a11y-media-has-caption -->
<audio bind:this={audio}>
  <source src="sound.mp3" />
</audio>
