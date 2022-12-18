<script>
	import Connex from "@vechain/connex";

	async function getBlock() {
	  const connex = new Connex({
	    node: "https://mainnet.veblocks.net",
	    network: "main"
	  });
	  const block = await connex.thor.status.head.number;
	  return block;
	}

	let promise = getBlock();

	function handleClick() {
	  promise = getBlock();
	}
</script>
	
	<button on:click={handleClick}>
		get block
	</button>
	
	{#await promise}
		<p>...waiting</p>
	{:then number}
		<p>Block: {number}</p>
	{:catch error}
		<p style="color: red">{error.message}</p>
	{/await}