<div class="mdc-layout-grid u-layout--centered">
  <div class="wrapper">
    <span data-testid="american-units-label">🇺🇸 American units</span>
    <Switch bind:checked={standardUnitsSelected} data-testid="switch" on:change={switchUnits} style="margin: 0 1em;" />
    <span data-testid="standard-units-label">🌏 Standard units</span>
  </div>
</div>
{#if !standardUnitsSelected}
  <div class="mdc-layout-grid u-padding-top--zero">
    <div class="grid mdc-layout-grid__inner">
      <div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-2"></div>
      <div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-8 u-centered">
        <Card padded>
          ⚠️
          <br>
          American units are imprecise and possibly unreliable. A proper <a target="_blank" href="https://www.amazon.com/gp/product/B0885Q6S45/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B0885Q6S45&linkCode=as2&tag=darrylsnow-20&linkId=179c581af018cd97e5cdd2bfb9b7211f" style="display: contents;">kitchen scale</a> is small and worthy investment when it comes to baking.
        </Card>
      </div>
      <div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-2"></div>
    </div>
  </div>
{/if}

<script>
  import { getContext } from 'svelte'
  import Card from '@smui/card/bare.js'
  import '@smui/card/bare.css'
  import Switch from '@smui/switch/bare.js'
  import '@smui/switch/bare.css'
  import { recipe } from '../store.js'

  let currentRecipe
  let newRecipe
  let standardUnitsSelected

  let updateRecipe = getContext('updateRecipe')

  recipe.subscribe((actualRecipe) => {
    currentRecipe = actualRecipe
    standardUnitsSelected = actualRecipe.useStandardUnits
  })

  const switchUnits = () => {
    newRecipe = Object.assign(currentRecipe, {
      useStandardUnits: standardUnitsSelected
    })
    recipe.set(newRecipe)
    updateRecipe('')
  }

</script>
