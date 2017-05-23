## miner package problems

- Need to convert to "CP437" encoding; see:
  <https://github.com/py3minepi/py3minepi/blob/master/mcpi/util.py>

  - flatten maybe turns iterators to lists
  - bytestring using cp437 encoding
  - cp437 == "extended ascii"

- Need care regarding delay between send and receive

- Need care about how many commands to send w/o overloading the
  minecraft server

- Painful to have to write out x,y,z, etc.; maybe "flatten" that turns
  whatever into a single vector of integers, like `unlist(list(...))`

- Don't totally know whether the server will send back a "Fail"
  response or nothing, and things hang if you try to get a message and
  there isn't one to get.
