<!-- BarCode.svelte -->
<script>
    import { setContext, onMount, afterUpdate } from 'svelte';
    import JsBarcode from "jsbarcode";
    let canvasId = generateRandomId();
    export let barcode;
    export let size;
    export let palette;
    let barcodeData = { barcode: "", size: 0, palette: "" };
  
    const palettes = {
      "Default": { bgColour: "white", fgColour: "black" },
      "Inverted": { bgColour: "black", fgColour: "white" },
      "Palette 2": { bgColour: "#0063B2FF", fgColour: "#9CC3D5FF" },
      "Inverted 2": { bgColour: "#9CC3D5FF", fgColour: "#0063B2FF" },
      "Palette 3": { bgColour: "#00203FFF", fgColour: "#ADEFD1FF" },
      "Inverted 3": { bgColour: "#ADEFD1FF", fgColour: "#00203FFF" },
    };
  
    function generateBarCode() {
      const canvas = document.getElementById(canvasId);
      JsBarcode(canvas, barcodeData.barcode, {
        format: "CODE128",
        height: barcodeData.size,
        displayValue: true,
        background: palettes[barcodeData.palette].bgColour,
        lineColor: palettes[barcodeData.palette].fgColour,
      });
    }
  
    setContext("BarCode", { generateBarCode });

    function generateRandomId() {
        return 'barcode-canvas-' + Math.random().toString(36).substr(2, 9);
    }

    onMount(() => {
        generateBarCode();
    });

    // Use afterUpdate to observe changes in barcode, size, or palette
    afterUpdate(() => {
        generateBarCode();
    });

    $: {
        barcodeData = { barcode, size, palette };
    }
</script>

{#if size.length > 0}
    <canvas id={canvasId}></canvas>
{:else}
  Please add a value to the barcode
{/if}
