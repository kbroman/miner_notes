world.getBlock -> "1"
world.getBlockWithData -> "1,0"
world.setBlock
world.setBlocks
world.getBlocks

world.getPlayerIds()
world.getPlayerEntityId(playerName) <- doesn't exist

world.postToChat(message)
world.saveCheckpoint()      [minecraft:Pi only]
world.restoreCheckpoint()   [minecraft:Pi only]
world.setting(setting, status) [minecraft:Pi only]
settings = world_immutable 0/1
           nametags_visible 0/1

player.getPos()
player.setPos(x,y,z)
player.getTile()
player.setTile(x,y,z)

player.setting(setting, status) [minecraft:pi only]
autojump true/false

player.getRotation()
player.getPitch()
player.getDirection()  [vector of three values separated by commas]

player things can also be applied to an entity
...it'd be good to have these be single functions that either use player or a particular entity
....it'd be good to have one function that returns rotation, pitch, and direction

entity.getPos(id)
entity.setPos(id,x,y,z)
entity.getTile(id)
entity.setTile(id,x,y,z)

events:
events.block.hits()
events.clear()
events.chat.posts()

[block hits must be with sword and you need to press left-click and
right-click together for some reason]


camera stuff is minecraft:pi only

---

world.getPlayerIds()
[results separated by vertical bars]

chat.post(raw_char_string)
e.g. chat.post(hello) not chat.post("hello")

player.getPos()
player.getTile()
entity.getPos(id)    <- id is an integer, as returned by world.getPlayerIds()
entity.getTile(id)
[results separated by commas]

If the thing doesn't work, the message back is "Fail"

world.getBlock
world.getBlockWithData
[returns id,style (separated by comma)]
world.getBlocks
[returns ids separated by commas as one long array]
z <- miner:::mc_sendreceive("world.getBlocks(1,1,1,3,4,2,0)", mc)
z <- as.numeric(strsplit(z, ",")[[1]])
z <- aperm(array(z, dim=c(2,3,4)), c(2,3,1))


world.setBlock
world.setBlocks
[set blocks sets them all to the same value; each can take id or id,style]
style = "blockData"
