---
title: Optimising ShreddedPaper
layout: default
parent: ShreddedPaper
---

# Optimising ShreddedPaper

Various changes you can make to improve the performance of ShreddedPaper

### netty-threads (required change for 250+ players)

Increasing the number of netty threads allows the server to handle more packets.
If the server does not have enough netty threads, the tps will start to drop
while the server tries to send more packets.

```yml
# spigot.yml
settings:
  netty-threads: 32
```

### maximum-trackers-per-entity

When there are a signficiant number of players in such a small area that they
can all see eachother, a lot of resources are spent rendering each player to
eachother at an exponential rate. Cap the number of players each player can see.
Increasing `tracker-full-update-frequency` also decreases how often an expensive
recalculation of what player can be seen is performed.

```yml
# shreddedpaper.yml
optimizations:
  maximum-trackers-per-entity: 200
  tracker-full-update-frequency: 40
```

### disable-vanish-api

The Bukkit vanish api (`Player.hidePlayer`) is inefficient. If you aren't using
it, disable it.

```yml
# shreddedpaper.yml
optimizations:
  disable-vanish-api: true
```

### ticks-per

Trying to spawn mobs is expensive. Reducing how often they try to spawn saves a
lot of resources.

```yml
# bukkit.yml
ticks-per:
  animal-spawns: 400
  monster-spawns: 400
  water-spawns: 400
  water-ambient-spawns: 400
  water-underground-creature-spawns: 400
  axolotl-spawns: 400
  ambient-spawns: 400
```

### simulation-distance

The less chunks you're ticking, the more performant the server.

```yml
# server.properties
simulation-distance=2
```

### view-distance

The less chunks you're sending the players, the more performant the server.

```yml
# server.properties
view-distance=8
```