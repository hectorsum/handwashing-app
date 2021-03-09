<script>
  import ProgressBar from './ProgressBar.svelte'
  const totalSeconds = 20;
  let secondLeft = totalSeconds;
  let isRunning = false;
  $: progress = ((totalSeconds-secondLeft) / totalSeconds) * 100;
  function startTimer(){
    isRunning=true;
    const timer = setInterval(() => {
      secondLeft-=1;
      if(secondLeft===0){
        clearInterval(timer)
        isRunning=false;
      }
    },1000);
  }
</script>
<style>
  h2{
    margin:0;
  }
  .start{
    background-color: rgb(154,73,73);
    width:100%;
    margin:10px 0px;
  }
  .start[disabled]{
    background-color: rgb(194,194,194);
    cursor: not-allowed;

  }
</style>
<div bp="grid">
  <h2 bp="offset-5@md 4@md 12@sm">
    Seconds left: {secondLeft}
  </h2>
</div>
<ProgressBar progress={progress}/>
<button disabled={isRunning} on:click={startTimer} class="start">
  Start
</button>