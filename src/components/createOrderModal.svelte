<script>
	import { onMount } from 'svelte';
	import { createEventDispatcher } from 'svelte';
	let open = false;
	const handleToggleModal = () => {
		open = !open;
	};
	const dispatch = createEventDispatcher();

	let dataRetrive = [];

	let order_id,id,
		customer = '',
		country = '',
		address = '',
		product_title = '',
		product_description = '',
		date,
		status = 'Prepared';

	const createOrder = async () => {
		const response = await fetch('https://my-json-server.typicode.com/Ved-X/assignment/orders');
		const data = await response.json();
		dataRetrive = data;
		order_id = dataRetrive[dataRetrive.length - 1].order_id + 1;
		console.log(order_id);

//getting current date
		var today = new Date();
		var yyyy = today.getFullYear();
		let  mm = today.getMonth() + 1; // Months start at 0!
		let dd =today.getDate();
    let day,month;
		if (dd < 10) day = ('0' + dd);
		if (mm < 10) month = ('0' + mm);

		date = day + '/' + month + '/' + yyyy;

    console.log(date);

		const req = await fetch(
			'https://my-json-server.typicode.com/Ved-X/assignment/orders?',
		  {
		    method:"POST",
		    body:JSON.stringify({
          order_id,
		      customer,
		      country,
		      address,
		      product_title,
		      product_description,
          date,
		      status,
		    })
		  }
		  );
	};
</script>

<button
	on:click={() => handleToggleModal()}
	class="bg-blue-600 text-white w-full text-xs p-2 px-2 rounded-lg">create orders</button
>

{#if open}
	<div
		class="modal z-50 fixed w-full h-full top-0 left-0 flex items-center justify-center p-8 lg:p-0"
	>
		<div class="modal-overlay fixed w-full h-full bg-gray-900 opacity-50" />
		<div
			class="bg-white w-full lg:h-max lg:w-1/2  mx-auto rounded-lg shadow-xl z-50 overflow-y-auto"
		>
			<div class="flex justify-between items-center head bg-gray-100 py-2 px-8 font-semibold">
				Create Orders
				<button
					class="p-2 bg-gray-200 hover:bg-gray-300 rounded-full ml-4"
					on:click={() => handleToggleModal()}
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						height="24px"
						viewBox="0 0 24 24"
						width="24px"
						fill="#000000"
						><path d="M0 0h24v24H0V0z" fill="none" /><path
							d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12 19 6.41z"
						/></svg
					>
				</button>
			</div>
			<div class="content p-8 text-sm">
				<div class="p-2">
					<label class="font-semibold" for="customer_name">Customer Name:</label>
					<input
						class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
						type="text"
						placeholder="john"
						bind:value={customer}
					/>
				</div>
				<div class="p-2">
					<label class="font-semibold" for="customer_name">Country: </label>
					<input
						class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
						type="text"
						placeholder="India"
						bind:value={country}
					/>
				</div>
				<div class="p-2">
					<label class="font-semibold" for="customer_name">Address:</label>
					<input
						class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
						type="text"
						placeholder="address"
						bind:value={address}
					/>
				</div>
				<div class="p-2">
					<label class="font-semibold" for="customer_name">Product title:</label>
					<input
						class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
						type="text"
						placeholder=""
						bind:value={product_title}
					/>
				</div>
				<div class="p-2">
					<label class="font-semibold" for="customer_name">Product description:</label>
					<input
						class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
						type="text"
						placeholder=""
						bind:value={product_description}
					/>
				</div>

				<div class="flex justify-center mt-4">
					<button
						type="submit"
						on:click={createOrder}
						class="bg-transparent hover:bg-green-500 text-green-700 font-semibold hover:text-white py-2 px-8 border border-green-500 hover:border-transparent rounded"
						>Submit</button
					>
				</div>
				<slot name="body" />
			</div>
		</div>
	</div>
{/if}
