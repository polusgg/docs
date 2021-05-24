
Game Option Entry format:

|    Type   |     Name      |                       Description                       |
|-----------|---------------|---------------------------------------------------------|
| `bool`    | Direction     | The direction of the packet. True if towards the client |
| `UInt8`   | Packet Type   | The type of the root game packet                        |
| `UInt8`   | Packet Length | The size of the packet                                  |
| `UInt8[]` | Packet        | The packet contents                                     |
