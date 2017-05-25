## miner package ideas

- `item_info`: take `id` or `name` and return rows from `mc_items1;
   use `grep` for `name` if no exact match.
   Could also take `id:style` as a character string.

- `player.getOrientation` that returns (Rotation,Pitch,Direction),
   though note that direction is a vector of 3 values

- I've been focusing on
  [RaspberryJuice](https://dev.bukkit.org/projects/raspberryjuice)
  with [Spigot](https://www.spigotmc.com), but it seems one can do all
  of this using an alternate method:
  [RaspberryJam](https://github.com/arpruss/raspberryjammod) with
  [Minecraft Forge](https://mcforge.readthedocs.io/en/latest/). If
  we're ambitious, we could an R package for each, or a single package
  that can be used with both.
