<style>
	
	button {
		font: inherit;
		padding: 0.15rem 0.5rem;
		background-color: lightcoral;
		color: white;
		cursor: pointer;
	}

	button:hover,
	button:active{
		box-shadow:rgba(1px, 1px, 6px, 0.26)
	}
</style>

<button on:click>
	<slot/>
</button>