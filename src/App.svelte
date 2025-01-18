<script>
  import Window from "./components/Window.svelte";

  // Handle responsive iframes for embeds
  import pym from "pym.js";

  new pym.Child({
    polling: 500,
  });

  let width;

  let unmitigated = 34111;
  let mitigated = 9666;
  let unit = 100;
</script>

<Window />
<!-- Outer div must have class 'chart-container' don't change -->
<div class="chart-container">
  <h1 class="headline">
    The vast majority of Louisiana properties with multiple flood insurance
    claims have not been mitigated
  </h1>
  <p class="dek">
    More than 43,000 properties in Louisiana have had multiple National Flood
    Insurance (NFIP) claims across the history of the program. Of those, only
    22% have received some form of <span class="mitigated">mitigation</span>,
    such as raising homes, improving drainage or constructing levees.
  </p>

  <div class="legend dek">
    <div class="item">🏠 = 100 properties</div>
    <div class="item">
      <div class="icon mitigated"></div>
      Mitigated
    </div>

    <div class="item">
      <div class="icon unmitigated"></div>
      Unmitigated
    </div>
  </div>

  <p class="sr-only">
    Chart showing the vast majority of Louisiana properties with multiple
    National Flood Insurance Program (NFIP) claims are unmitigated, represented
    by orange icons. Of the over 43,000 properties, only 22% are mitigated,
    shown in green, with each icon representing 100 properties.
  </p>

  <div id="g-viz" bind:clientWidth={width}>
    <div class="section">
      {#each Array(Math.round(mitigated / unit)) as x}
        <div class="icon mitigated">🏠</div>
      {/each}

      {#each Array(Math.round(unmitigated / unit)) as x}
        <div class="icon unmitigated">🏠</div>
      {/each}
    </div>
  </div>

  <div class="credit">
    Data: <a
      target="_blank"
      href="https://www.fema.gov/openfema-data-page/nfip-multiple-loss-properties-v1"
      >FEMA</a
    >; Graphic by Jared Whalen /
    <a target="_blank" href="https://agwaterdesk.org/">Ag & Water Desk</a>
  </div>
</div>

<style lang="scss">
  .chart-container {
    max-width: 800px;
    width: 100%;
    padding: 2px;
  }

  .legend {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    .item {
      display: flex;
      align-items: center;
      gap: 0.25rem;

      .icon {
        width: 20px;
        height: 20px;
      }
    }
  }

  .dek {
    .mitigated {
      color: #6da34d;
      font-weight: bold;
    }
  }

  #g-viz {
    position: relative;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    gap: 0.25rem;

    .section {
      display: flex;
      flex-wrap: wrap;
      gap: 0.15rem;
      position: relative;
    }
  }

  .icon {
    font-size: 13px;
    width: 22px;
    height: 22px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 2px;

    &.mitigated {
      background: #6da34d99;
    }

    &.unmitigated {
      background: #f1b82d99;
    }
  }
</style>
