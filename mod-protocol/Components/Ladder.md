Ladders are the PNO equivalent of ladders.

This component contains Data:

|Type|Name|Description|
|-|-|-|
|`PackedUInt32`|SpriteResourceID|The resource ID for the ladder|
|`Byte`|ID|This ladder's ID|
|`Vector2`|TopPosition|Top position of the ladder|
|`Vector2`|BottomPosition|Bottom position of the ladder|
| | | Below, the data that will be sent once we have a proper console system |
|`Byte`|Size|How many people have access to the console at a time|
|`Byte[]`|Player IDs|Who has access to the console|

Sends the same rpcs as normal ladders would.