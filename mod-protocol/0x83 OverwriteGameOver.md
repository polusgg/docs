# `0x83` Root - OverwriteGameOver

```cs
public enum WinSounds {
  CrewmateWin = 1,
  ImpostorWin = 2,
  Disconnect = 3,
  NoSound = 4,
}
```

## S2C (Request)
| Type | Name | Description |
|------|------|-------------|
| `String` | TitleText | The title text. e.g. "Victory" |
| `String` | SubtitleText | The subtitle text e.g. "There is 1 Impostor among us" |
| `Byte[4]` | BackgroundColor | The color of the background gradient |
| `Byte` | Length | How many players are on your team |
| `Byte[]` | YourTeam | A PlayerID[] containing the player IDs of players to display |
| `boolean` | DisplayQuit | If false, the quit button will be hidden |
| `boolean` | DisplayPlayAgain | If false, the play again button will be hidden |
| `Byte` | WinSound | The sound played on a win or loss |
| `PackedUInt32` | CustomSound | If a custom sound is set, this |

```
NOTE: This does __not__ display the game over screen. Instead this overwrites the data for the *next* game over screen. It will almost always be sent just before the root end game packet.

Flow:
 - 0x91 OGO <#data>
 - 0x08 EndGame (EndGameReason ignored) (replaced with #data)
 - 0x08 EndGame (EndGameReason NOT ignored)
 - 0x91 OGO <#data2>
 - 0x91 OGO <#data3>
 - 0x08 EndGame (EndGameReason ignored) (replaced with #data3)
 - 0x91 OGO <#data4>
 - 0x08 EndGame (EndGameReason ignored) (replaced with #data4)
```
