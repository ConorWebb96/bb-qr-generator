<!-- QRCode.svelte -->
<script>
  import { setContext } from 'svelte';
  import QRious from 'qrious';
  export let url;
  export let size;
  export let errorCorrection;
  export let palette;
  export let mimeType;

  let qrCodeUrl = '';
  const palettes = {
    "Default": { bgColour: "white", fgColour: "black" },
    "Inverted": { bgColour: "black", fgColour: "white" },
    "Palette 2": { bgColour: "#0063B2FF", fgColour: "#9CC3D5FF" },
    "Inverted 2": { bgColour: "#9CC3D5FF", fgColour: "#0063B2FF" },
    "Palette 3": { bgColour: "#00203FFF", fgColour: "#ADEFD1FF" },
    "Inverted 3": { bgColour: "#ADEFD1FF", fgColour: "#00203FFF" },
  };

  function generateQRCode(url, size, palette, errorCorrection, mimeType) {
    const qrCode = new QRious({
      value: url,
      size: size,
      foreground: palettes[palette].fgColour,
      background: palettes[palette].bgColour,
      level: errorCorrection,
      mime: mimeType,
    });
    qrCodeUrl = qrCode.toDataURL(mimeType);
  }

  setContext("QRCodeComponent", { generateQRCode });

  $: {
    generateQRCode(url, size, palette, errorCorrection, mimeType); // Regenerate QR code when url changes
  }
</script>
{#if qrCodeUrl}
  <div>
    <img src={qrCodeUrl} alt="QR Code" />
  </div>
{:else}
  <p>Empty</p>
{/if}

<style>

</style>