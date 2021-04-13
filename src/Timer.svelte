<script>
  import ProgressBar from "./ProgressBar.svelte";

  const totalSeconds = 20;
  let secondsLeft = totalSeconds;
  let isRunning = false;
  $: progress = ((totalSeconds - secondsLeft) / totalSeconds) * 100;

  const resetTimer = () => {
    isRunning = true;
    const timer = setInterval(() => {
      secondsLeft--;
      if (secondsLeft == 0) {
        clearInterval(timer);
        isRunning = false;
        secondsLeft = totalSeconds;
      }
    }, 1000);
  };
</script>

<div bp="grid">
  <h2 bp="offset-5@md 4@md 12@sm">Seconds Left:{secondsLeft}</h2>
</div>
<ProgressBar {progress} />

<div bp="grid">
  <button
    disabled={isRunning}
    on:click={resetTimer}
    bp="offset-5@md 4@md 12@sm"
    class="start">Start</button
  >
</div>

<style>
  h2 {
    margin: 0;
  }
  .start {
    background-color: rgb(154, 73, 73);
    width: 100%;
    margin: 10px 0;
  }
  .start[disabled] {
    background-color: rgb(194, 194, 194);
    cursor: not-allowed;
  }
</style>
