<script>
    export let label;
    export let placeholder;
</script>

<div class="p-2">
    <label class="font-semibold" for="customer_name">{label}</label>
    <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        type="text"
        placeholder={placeholder}
    />
</div>