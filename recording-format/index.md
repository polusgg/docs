
File Format:

|        Type         |       Name        |                        Description                        |
|---------------------|-------------------|-----------------------------------------------------------|
| `UInt32`            | Version           | The version of the mod                                    | 
| `UInt8`             | Player Count      | The number of players in the game at the time of starting |
| `Player[]`          | Players           | The players in the lobby                                  |
| `UInt8`             | Game Option Count | The number of Game Options                                |
| `GameOptionEntry[]` | Game Options      | The game options                                          |
| `UInt32`            | Packet Count      | The number of packets                                     |
| `Packet[]`          | Packets           | The packet log                                            |
