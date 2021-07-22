<script>
	import Button from './Button.svelte';
	import Product from "./Product.svelte";
	import Cart from "./Cart.svelte";

	let title = '';
	let price = '0';
	let description = '';

	let products = [];
	let cartItems = [];

	const setTitle =(e) => {
		title = e.target.value;
	}

	const createProduct =(e) => {
		const newProduct = {
			title,
			price,
			description,
		}
		products = products.concat(newProduct);
	}

	const addToCart =(e) => {
		const selectedTitle = e.detail;
		
		cartItems = cartItems.concat({
			...products.find(prod=> prod.title === selectedTitle)
		});
		console.log(cartItems)
	}
</script>

<section>
	<Cart items={cartItems} />
	<hr/>
</section>

<section>
	<div>
		<label for='title'>Title</label>
		<input type="text" id='title' value="{title}" on:input="{setTitle}" />
	</div>
	<div>
		<label for='prce'>Price</label>
		<input type="number" id="price" bind:value={price} />
	</div>
	<div>
		<label for='description'>Description</label>
		<textarea rows="3" id="description" bind:value={description} />
	</div>
	<Button on:click={createProduct}>Submit</Button>
</section>
<section>
	{#if products.length===0}
		<p>No product were added yet!</p>
	{:else}
		{#each products as product}
			<Product  
				productTitle={product.title}
				productPrice={product.price}
				productDescription={product.description}
				on:addcart={addToCart}
			/>
		{/each}
	{/if}
</section>


<style>
	section{
		width: 30rem;
		margin: auto;

	}

	label, 
	textarea, 
	input{
		width: 100%;
	}

	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
