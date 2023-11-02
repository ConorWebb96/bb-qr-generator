<!-- App.svelte -->
<script>
  import { getContext } from "svelte";
  import QRCode from "./QRCode.svelte";
  import BarCode from "./BarCode.svelte";

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  export let genType;
  export let url;
  export let barcode;
  export let size;
  export let errorCorrection;
  export let palette;
  export let mimeType;
</script>

<div use:styleable={$component.styles}>
  {#if genType == "qrCode"}
     <QRCode 
       {url} 
       {size} 
       {errorCorrection}
       {palette}
       {mimeType}
     />
  {:else}
     <BarCode 
       {barcode} 
       {size} 
       {palette} 
     />
  {/if}
</div>

<style>
  /* Add your styling here */
</style>