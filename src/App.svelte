<script>
	import Navbar from "./Navbar.svelte"
	import products from "./products"
	import { fade } from "svelte/transition"
	import { flip } from "svelte/animate"

	let selectedType = ""
	let cart = []
	let isCartVisible = false
	
	$: total = cart.reduce((sum, item) => sum + item.price * item.quantity, 0)

	const addToCart = (product) => {
		for (let item of cart) {
			if (item.id === product.id) {
			product.quantity += 1
			cart = cart
			return
			}
		}

		cart = [...cart, product]
	}
</script>

<Navbar bind:selected={selectedType} bind:isCartVisible/>

<main>
	{#if isCartVisible}
		<div class="cart">
			{#each cart as item}

			<div class="cart-item">
				<img width=50; height=50; src="pics/{item.image}" alt={item.name}/>
				<p>{item.quantity} ks</p>
				<p>{item.price * item.quantity} Kč</p>
			</div>
			{/each}
			<h2>Celková cena: {total} Kč</h2>
		</div>
	{/if}

	<div class="products">
		{#each products.filter(p => selectedType == "" || p.type == selectedType) as product(product.name)}
			<div 
				class="product" 
				in:fade={{ duration: 200 }} 
				out:fade={{ duration: 200 }} 
				animate:flip={{ duration: 200 }}
			>
				<img src="pics/{product.image}" alt="{product.name}">
				<p class="name">{product.name}</p>
				<br>
				<p class="price">Cena: {product.price} Kč</p>
				<br>
				<p class="description"> {product.description} </p>
				<img on:click={() => addToCart(product)} class="plus-icon" src="icons/plus_icon.svg" alt="add product">		
			</div>
		{/each}
	</div>
</main>

<style>
	.cart{
		position: fixed;
		left: 50%;
		top: 50%;
		transform: translate(-50%,-50%);
		z-index: 99;
		padding: 10rem;
		background-color: #866083;
		color: white;
		opacity: 90%;
		width: 400px;
		height: 200px;
	}

	.cart-item{
		display:grid;
		grid-template-columns: repeat(3, 1fr);
	}
	
	.cart-item img{
		background-color: #fff4f8;
		object-fit: contain;
	}

	.products {
		display: grid;
		width: 80%;
		margin: auto;
		grid-template-columns: repeat(4,1fr);
		grid-column-gap: 4rem;
		grid-row-gap: 4rem;
	}

	.product {
		background-color: white;
		padding: 2rem;
		text-align: center;
		border-radius: 10px;
		box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
	}

	.product img {
		width: 150px;
		height: 150px;
		object-fit: contain;
	}

	.product .name {
		font-weight: bold;
		font-size: 25px;
		text-transform: capitalize;
	}

	.product .price {
		font-size: 20px;
	}

	.product .description{
		height: 100px;
	}

	.product .plus-icon {
		width: 50px;
		height: 50px;
		margin: 20px 0;
		cursor: pointer;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>