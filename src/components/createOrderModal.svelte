<script>
	import { createEventDispatcher } from 'svelte';
	import FormElement from './formElement.svelte';
	let open = false;
	const handleToggleModal = () => {
		open = !open;
	};
	const dispatch = createEventDispatcher();

	function createOrder() {
		alert('submit clicker');
	}
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
				<FormElement label="Customer Name:" placeholder="john" />
				<FormElement label="Country:" placeholder="India" />
				<FormElement label="Address:" placeholder="address" />
				<FormElement label="Product title:" placeholder="" />
				<FormElement label="Product description:" placeholder="" />
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
