## Minecraft API notes

- World stuff

  ```
  world.getBlock -> "1"
  world.getBlockWithData -> "1,0"
  world.setBlock
  world.setBlocks
  world.getBlocks
  ```

- get player information

  ```
  world.getPlayerIds()
  world.getPlayerEntityId(playerName)  # (doesn't exist)
  ```

- chat/checkpoint/setting

  ```
  world.postToChat(message)
  world.saveCheckpoint()         # [minecraft:Pi only]
  world.restoreCheckpoint()      # [minecraft:Pi only]
  world.setting(setting, status) # [minecraft:Pi only]
  settings = world_immutable 0/1
             nametags_visible 0/1
  ```

- player position

  ```
  player.getPos()
  player.setPos(x,y,z)
  player.getTile()
  player.setTile(x,y,z)
  ```

- player setting

  ```
  player.setting(setting, status) # [minecraft:pi only]
  autojump true/false
  ```

- player orientation

  ```
  player.getRotation()
  player.getPitch()
  player.getDirection()  [vector of three values separated by commas]
  ```

- entity position etc (just like player position; maybe combine these
  into one set of functions); the id is as in the output of `world.getPlayerIds()`

  ```
  entity.getPos(id)
  entity.setPos(id,x,y,z)
  entity.getTile(id)
  entity.setTile(id,x,y,z)
  ```

- events

  ```
  events.block.hits()
  events.clear()
  events.chat.posts()
  ```


  [block hits must be with sword and you need to press left-click and
  right-click together for some reason]


- camera stuff is minecraft:pi only

---

### further details on the output of the API calls

- `world.getPlayerIds()`: results separated by vertical bars

- `chat.post(raw_char_string)` e.g. `chat.post(hello)` not `chat.post("hello")`

- `player.getPos()` and `entity.getPos(id)` and also `.getTile()`
  return a vector of numbers separated by commas

- If things don't work, the message back is (or may be) "Fail"

- `world.getBlock`, `world.getBlockWithData`: the latter returns
  `id,style` (separated by a comma)

- `world.getBlocks` returns ids only, separated by commas as one long
  vector. The order of things is a bit tricky.

  Something like:

  ```
  z <- miner:::mc_sendreceive("world.getBlocks(1,1,1,3,4,2,0)", mc)
  z <- as.numeric(strsplit(z, ",")[[1]])
  z <- aperm(array(z, dim=c(2,3,4)), c(2,3,1))
  ```


- `world.setBlock`, `world.setBlocks`: the latter sets them all to the
  same value. Each can take just an `id` or both `id` and `style`. (The
  API says "blockData" where I say "style".)
