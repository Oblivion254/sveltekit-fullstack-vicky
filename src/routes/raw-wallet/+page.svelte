<script lang="ts">
  import { PrivateKey } from "@bsv/sdk";

  let WIF: string;
  let address: String;
  let keyGenerated = false;

  function createKeys() {
    const privKey = PrivateKey.fromRandom();
    WIF = privKey.toWif();
    console.log("Private Key WIF format is ", WIF);
    address = privKey.toAddress();
    console.log("Your bitcoin address is ", address);
    keyGenerated = true;
  }

  function copyWIF(){
    var copyText = `Private Key WIF format is ${WIF}, Your bitcoin address is ${address}`;
    navigator.clipboard.writeText(copyText);
    console.log("Text Copied!");
  }
</script>

<section>
  <div class="flex flex-col mt-10 pt-10 w-full max-w-4xl p-5 mx-auto rounded-lg shadow-xl dark:bg-white/10 bg-white/30 ring-1 ring-gray-900/5 backdrop-blur-lg">
    <div class="flex justify-center">
      <button on:click={createKeys} class="bg-black text-white px-3 py-2 mb-2 rounded-lg"
        >Generate New Wallet Keys</button
        >
    </div>

    <div>
      <p>Private Key WIF format is: <span class="font-semibold">{WIF}</span></p>
    </div>

    <div>
      <p>Your Bitcoit address is: <span class="font-semibold">{address}</span></p>
    </div>
    {#if keyGenerated}
  <!-- this message is ephemeral; it exists because the page was rendered in
     response to a form submission. it will vanish if the user reloads -->
     <div class="flex flex-row-reverse"><button class="bg-gray-400 text-gray-700 shadow hover:shadow-md hover:text-slate-200 px-3 py-2 rounded" on:click={() => copyWIF()}>Copy</button>
     </div>
{/if}
  </div>
</section>
