# `0x89` PlayerControl - DespawnVents
## S2C (Request)
| Type | Name | Description |
| --- | --- | --- |
| `PackedUInt32` | VentCount | How many vents are in the list. |
| `Byte[]` | VentIDs | Each vent to be destroyed. |

Destroys all of the vents listed on the ship.