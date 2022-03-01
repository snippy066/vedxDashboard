<script>
  import { onMount } from 'svelte';
  import DataDisplay from './dataDisplay.svelte';

  let dashData=[];
  let val ="";

  const load=async () => {

    const arr=[];
    if(val!=""){
      arr.push(val);
    }

		const response = await fetch('https://my-json-server.typicode.com/Ved-X/assignment/orders?'+val);
		const data = await response.json();
    dashData=data;
		console.log(data);
	}


  onMount(load);
</script>

<div class="flex justify-between items-center mt-4">
<div class="relative mx-0 text-gray-600 items-center w-full">
    <div class="absolute p-2">
    <svg class="text-gray-600 h-4 w-4 fill-current" xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px"
        viewBox="0 0 56.966 56.966" style="enable-background:new 0 0 56.966 56.966;" xml:space="preserve"
        width="512px" height="512px">
        <path
          d="M55.146,51.887L41.588,37.786c3.486-4.144,5.396-9.358,5.396-14.786c0-12.682-10.318-23-23-23s-23,10.318-23,23  s10.318,23,23,23c4.761,0,9.298-1.436,13.177-4.162l13.661,14.208c0.571,0.593,1.339,0.92,2.162,0.92  c0.779,0,1.518-0.297,2.079-0.837C56.255,54.982,56.293,53.08,55.146,51.887z M23.984,6c9.374,0,17,7.626,17,17s-7.626,17-17,17  s-17-7.626-17-17S14.61,6,23.984,6z" />
      </svg></div>
    <input
     class="border-2  border-gray-300 bg-white h-9 w-1/2 px-9 pr-16 rounded-lg text-sm focus:outline-none"
      type="search" 
      bind:value={val}
      name="search" placeholder="Search">
    <button type="submit" class="absolute right-0 top-0 mt-5 mr-4">
      
    </button>
  </div>

  <div>
      Filter
  </div>

</div>

<DataDisplay {dashData}/>