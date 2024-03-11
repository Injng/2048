<script lang="ts">
    import Tile from "$lib/Tile.svelte";
    import { tick } from 'svelte';
    
    // keep track of the board and where there are no tiles 
    let board: number[][];
    board = [
        [0, 0, 0, 0],
        [0, 0, 0, 0],
        [0, 0, 0, 0],
        [0, 0, 0, 0]
    ];
    let zeroes: [number, number][] = [];
    
    // update the array where there are no tiles
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
    
    // create a new tile where there are no tiles
    function newTile() {
        updateZeroes();
        if (zeroes.length == 0) {
            return;
        }
        let [i, j] = zeroes[Math.floor(Math.random() * zeroes.length)];
        board[i][j] = Math.random() < 0.9 ? 2 : 4;
        board = board;
    }

    /**
     * Finds the farthest position a tile can slide to in a given direction.
     *
     * @param tile - The starting [x, y] position of the tile.
     * @param direction - The direction to slide (0=north, 1=east, 2=south, 3=west).
     * @returns The farthest [x, y] position the tile can slide to.
     */
    function findFarthest(tile: [number, number], direction: number): [number, number] {
        let [x, y] = tile;
        if (direction == 0) {
            if (x == 0) return [x, y];
            for (let i = x - 1; i >= 0; i--) {
                if (board[i][y] == board[x][y]) return [i, y];
                else if (board[i][y] != 0) return [i + 1, y];
            }
            return [0, y];
        } else if (direction == 1) {
            if (y == 3) return [x, y];
            for (let i = y + 1; i <= 3; i++) {
                if (board[x][i] == board[x][y]) return [x, i];
                else if (board[x][i] != 0) return [x, i - 1];
            }
            return [x, 3];
        } else if (direction == 2) {
            if (x == 3) return [x, y];
            for (let i = x + 1; i <= 3; i++) {
                if (board[i][y] == board[x][y]) return [i, y];
                else if (board[i][y] != 0) return [i - 1, y];
            }
            return [3, y];
        } else if (direction == 3) {
            if (y == 0) return [x, y];
            for (let i = y - 1; i >= 0; i--) {
                if (board[x][i] == board[x][y]) return [x, i];
                else if (board[x][i] != 0) return [x, i + 1];
            }
            return [x, 0];
        } else {
            throw new Error("Invalid direction");
        }
    }
    
    /**
     * Moves all tiles on the board in the given direction, combining
     * tiles when they collide. Updates board state after moving.
     *
     * @param e - KeyboardEvent triggered by arrow key press
     */
    function moveTiles(e: KeyboardEvent) {
        // direction: 0=north, 1=east, 2=south, 3=west
        let direction: number = -1;
        switch (e.key) {
            case "ArrowDown":
                direction = 2;
                break;
            case "ArrowUp":
                direction = 0;
                break;
            case "ArrowLeft":
                direction = 3;
                break;
            case "ArrowRight":
                direction = 1;
                break;
        }
        if (direction == -1) return;

        // pass through the board and slide tiles in the given direction
        for (let i = 0; i < 4; i++) {
            for (let j = 0; j < 4; j++) {
                if (board[i][j] == 0) continue;
                let [x, y] = findFarthest([i, j], direction);
                console.log("reached");
                if (x == i && y == j) continue;
                else if (board[x][y] == 0) board[x][y] = board[i][j];
                else if (board[x][y] == board[i][j]) board[x][y] *= 2;
                console.log("hello");
                console.log(board[x][y]);
                console.log(board[i][j]);
                board[i][j] = 0;
            }
        }
        newTile();
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

<svelte:window on:keydown|preventDefault={moveTiles} />