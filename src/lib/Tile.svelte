<script lang="ts">
    export let num: number = 0;
    
    const colors: { [key: number]: string } = {
        0: "nord4",
        2: "nord13",
        4: "nord12",
        8: "nord11",
        16: "nord14",
        32: "nord15",
        64: "nord10",
        128: "nord9",
        256: "nord8",
        512: "nord7",
        1024: "nord5",
        2048: "nord6",
    };
</script>

<div class= "bg-{colors[num]} grid place-items-center m-2 text-7xl">
    {num == 0 ? "" : num}
</div>