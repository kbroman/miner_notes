## miner package ideas

- `item_info`: take `id` or `name` and return rows from `mc_items1;
   use `grep` for `name` if no exact match.
   Could also take `id:style` as a character string.

- `player.getOrientation` that returns (Rotation,Pitch,Direction),
   though note that direction is a vector of 3 values
