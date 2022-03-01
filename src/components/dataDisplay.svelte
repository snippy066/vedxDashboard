<script>
 export let dashData;
</script>


<table class="shadow-md bg-white mx-2 mt-4 rounded-lg w-full">
    <tr class="text-xs bg-blue-200">
      <th class="rounded-l-lg text-left px-6 py-2">ORDER ID</th>
      <th class=" text-left px-6 py-2">CUSTOMER</th>
      <th class=" text-left px-6 py-2">ADDRESS</th>
      <th class=" text-left px-6 py-2">PRODUCT</th>
      <th class=" text-left px-6 py-2">DATE ORDER</th>
      <th class="rounded-r-lg text-left px-6 py-2">STATUS</th>
    </tr>

    {#each dashData as data}
    <tr class="text-xs">
      <td class=" px-6 py-2">{data.order_id}</td>
      <td class=" px-6 py-2">{data.customer}</td>
      <td class=" px-6 py-2">{data.address}</td>
      <td class=" px-6 py-2">{data.product_title}</td>
      <td class=" px-6 py-2">{data.date}</td>
      <td class=" px-6 py-2">
        {#if data.status=="Delivered"}
          <div class="bg-blue-100 w-fit rounded-lg p-1 text-xs text-blue-600 ">{data.status}</div>
        {:else if data.status=="Prepared"}
        <div class=" bg-red-100 w-fit rounded-lg p-1 text-xs text-red-600 ">{data.status}</div>
        {:else if data.status=="Prepared"}
        <div class="bg-green-100 w-fit rounded-lg p-1 text-xs text-green-600 ">{data.status}</div>
        {/if}
          </td>
    </tr>
    {/each}

  </table>