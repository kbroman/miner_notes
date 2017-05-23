## miner package questions

- Can/should we deviate from the API? In some ways it's cumbersome
  (for example, `entity.getPos(id)` and `player.getPos()`
   could just be one function; `setBlocks` could optionally take an array
   and then repeatedly call `setBlock`)

- Can we make the server connection a global variable somehow?
  (repeatedly having to include it in the function calls can be a bit
  of a pain)
