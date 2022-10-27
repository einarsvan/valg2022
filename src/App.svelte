<script>
  // Animation constants
  const animationIntervalMS = 6000; // Number/Integer
  const animationDurationS = 1.4; // Number/Float
  const animationDelayBetweenMS = 200; // Number/Int

  const front = ['V', 'A', 'L', 'G'];
  const back = ['2', '0', '2', '2'];

  let frontContainer;
  let backContainer;

  /**
   * Animate the children (span) of a given container 
   * @param container
   */
  const animateEachChild = container => {    

    if(!container) return;

    // Find all children of container
    const list = container.childNodes;
    list.forEach((element, i) => {
      // Change the class for each child, with a delay
      setTimeout(()=>{
        if(element.classList.contains('hide')){
          element.classList.remove('hide');
        } else {
          element.classList.add('hide');
        }

      }, animationDelayBetweenMS * i);
    });
  };

  const animationLoop = setInterval(()=> {
    animateEachChild(frontContainer);
    animateEachChild(backContainer);

  }, animationIntervalMS);

</script>

<main style="--animationDurationS:{animationDurationS}s">
  <div class="valg-22">
    <div class="cards">
      <div class="front" bind:this={frontContainer}>
        {#each front as letter}
          <span>{letter}</span>
        {/each}
      </div>
      <div class="back" bind:this={backContainer}>
        {#each back as letter}
          <span class="hide">{letter}</span>
        {/each}
      </div>
    </div>
    <div class="colored-box background-1"/>
    <div class="colored-box background-2"/>
    <div class="colored-box background-3"/>
  </div>

</main>

<style>
  main {
    margin: 2rem;
  }

  .valg-22 {
    position: relative;
    font-size: 60px;
    height: 5em;
    width: 5em;
  }

  .colored-box {
    position: absolute;
    width: 4em;
    height: 4em;
    opacity: 0.5;
  }

  .background-1 {
    z-index: 2;
    background-color: aqua;
    top: 0.5em;
    left: 0em;
  }
  .background-2 {
    z-index: 4;
    background-color: purple;
    right: 0em;
    bottom: 0em;
  }
  .background-3 {
    z-index: 6;
    background-color: yellow;
    left: 0.5em;
    bottom: 0.8em;
  }

  .cards {
    position: relative;
    background-color: rgba(1,1,1,0.9);
    color: white;
    top: 1em;
    left: 1em;
    width: 3em;
    height: 3em;
    z-index: 10;
  }

  .cards > div {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    justify-items: center;
    justify-content: center;
  }

  .cards span {
    display: inline-block;
    transition: rotate var(--animationDurationS), opacity var(--animationDurationS);
    transform-origin: center;
    opacity: 1;
  }
  .cards span.hide {
    rotate: y 90deg;
    opacity: 0;
  }

</style>
