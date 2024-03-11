<script lang="ts">
    import Tile from "$lib/Tile.svelte";
    
    let board: number[][];
    board = [
        [0, 0, 0, 0],
        [0, 0, 0, 0],
        [0, 0, 0, 0],
        [0, 0, 0, 0]
    ];
    let zeroes: [number, number][] = [];
    
    function updateZeroes() {
        zeroes = [];
        for (let i = 0; i < 4; i++) {
            for (let j = 0; j < 4; j++) {
                if (board[i][j] == 0) {
                    zeroes.push([i, j]);
                }
            }
        }
    } 
    
    function newTile() {
        updateZeroes();
        if (zeroes.length == 0) {
            return;
        }
        let [i, j] = zeroes[Math.floor(Math.random() * zeroes.length)];
        board[i][j] = Math.random() < 0.9 ? 2 : 4;
        board = board;
    }
</script>

<body>
    <div class="bg-nord1 h-10"> </div>
    <div class="bg-nord2 mx-auto m-4 h-[592px] w-[592px] grid grid-cols-4"> 
        <div class="bg-nord4 mt-[16px] ml-[16px] m-[8px] grid h-[128px] w-[128px]"> 
            {#if board[0][0] != 0}
                <Tile num={board[0][0]} />
            {/if}
        </div>
        <div class="bg-nord4 mt-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[0][1] != 0}
                <Tile num={board[0][1]} />
            {/if}
        </div>
        <div class="bg-nord4 mt-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[0][2] != 0}
                <Tile num={board[0][2]} />
            {/if}
        </div>
        <div class="bg-nord4 mt-[16px] mr-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[0][3] != 0}
                <Tile num={board[0][3]} />
            {/if}
        </div>

        <div class="bg-nord4 ml-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[1][0] != 0}
                <Tile num={board[1][0]} />
            {/if}
        </div>
        <div class="bg-nord4 m-[8px] grid h-[128px] w-[128px]">
            {#if board[1][1] != 0}
                <Tile num={board[1][1]} />
            {/if}
        </div>
        <div class="bg-nord4 m-[8px] grid h-[128px] w-[128px]">
            {#if board[1][2] != 0}
                <Tile num={board[1][2]} />
            {/if}
        </div>
        <div class="bg-nord4 mr-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[1][3] != 0}
                <Tile num={board[1][3]} />
            {/if}
        </div>

        <div class="bg-nord4 ml-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[2][0] != 0}
                <Tile num={board[2][0]} />
            {/if}
        </div>
        <div class="bg-nord4 m-[8px] grid h-[128px] w-[128px]">
            {#if board[2][1] != 0}
                <Tile num={board[2][1]} />
            {/if}
        </div>
        <div class="bg-nord4 m-[8px] grid h-[128px] w-[128px]">
            {#if board[2][2] != 0}
                <Tile num={board[2][2]} />
            {/if}
        </div>
        <div class="bg-nord4 mr-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[2][3] != 0}
                <Tile num={board[2][3]} />
            {/if}
        </div>

        <div class="bg-nord4 mb-[16px] ml-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[3][0] != 0}
                <Tile num={board[3][0]} />
            {/if}
        </div>
        <div class="bg-nord4 mb-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[3][1] != 0}
                <Tile num={board[3][1]} />
            {/if}
        </div>
        <div class="bg-nord4 mb-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[3][2] != 0}
                <Tile num={board[3][2]} />
            {/if}
        </div>
        <div class="bg-nord4 mb-[16px] mr-[16px] m-[8px] grid h-[128px] w-[128px]">
            {#if board[3][3] != 0}
                <Tile num={board[3][3]} />
            {/if}
        </div>
    </div>
</body>

<svelte:window on:keydown|preventDefault={newTile} />