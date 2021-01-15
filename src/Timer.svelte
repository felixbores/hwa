<script>
  import { createEventDispatcher } from 'svelte';
  import ProgressBar from './ProgressBar.svelte';

  $: progress = ((totalSeconds - secondsLeft) * 100) / totalSeconds;

  const eventDispatcher = createEventDispatcher();
  const totalSeconds = 20;
  let secondsLeft = totalSeconds;
  let isRunning = false;

  const handleStart = () => {
    isRunning = true;

    const timer = setInterval(() => {
      secondsLeft -= 1;
      if (secondsLeft === 0) {
        isRunning = false;
        secondsLeft = totalSeconds;
        clearInterval(timer);
        eventDispatcher('end');
      }
    }, 1000);
  };
</script>

<style>
  h2 {
    margin: 0;
  }
  .start {
    width: 100%;
    background-color: rgb(174, 73, 73);
    margin: 10px 0;
  }

  .start[disabled] {
    background-color: #c3c3c3;
    cursor: not-allowed;
  }
</style>

<div bp="grid">
  <h2 bp="offset-5@md 4@md 12@sm">Seconds Left: {secondsLeft}</h2>
</div>
<ProgressBar {progress} />
<div bp="grid">
  <button
    on:click={handleStart}
    disabled={isRunning}
    bp="offset-5@md 4@md 12@sm"
    class="start">Start</button
  >
</div>
