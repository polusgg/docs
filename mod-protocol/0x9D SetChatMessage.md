## Chat Alignment
| ID | Name |
|----|------|
| 0 | Left |
| 1 | Center |
| 2 | Right |

# `0x9D` Root - SetChatMessage

## S2C
| Type | Name | Description |
|------|------|-------------|
| `Byte[16]` | UUID | The unique identifier of the message in UUID format |
| `Byte` | Align | Where the message should appear in the chat window, see [Chat Alignment](#chat-alignment) |
| `String` | Name | The name of the author to appear as |
| `Boolean` | Dead | Whether the author is dead |
| `PackedUInt32` | Hat | The ID of the hat of the player |
| `PackedUInt32` | Skin | The ID of the skin of the player |
| `PackedUInt32` | Pet | The ID of the pet of the player |
| `Byte[4]` | ShadowColor | The shadow color of the author |
| `Byte[4]` | BodyColor | The body color at the author |
| `Boolean` | QuickChat | Whether the mesage is a quick chat message |
| `Byte[]` | MessageContent | The content of the message, can be  |