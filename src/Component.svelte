<!-- App.svelte -->
<script>
  import { getContext } from "svelte";
  import QRCode from "./QRCode.svelte";

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  export let url;
  export let size;
  export let errorCorrection;
  export let palette;
  export let mimeType;
</script>

<div use:styleable={$component.styles}>
  <QRCode 
    {url} 
    {size} 
    {errorCorrection}
    {palette}
    {mimeType}
  />
</div>

<style>
  /* Add your styling here */
</style>