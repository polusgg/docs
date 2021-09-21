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
| `Byte[16]` | MessageUUID | The unique identifier of the message in UUID format |
| `Byte` | Align | Where the chat message should appear in the chat window, see [Chat Alignment](#chat-alignment) |
| `String` | AuthorName | The name of the author to appear as sending the message |
| `Boolean` | AuthorAlive | Whether or not the author was alive sending the message, and thus how to display the message |
| `UInt32` | AuthorHat | The ID of the hat cosmetic of the author who sent the message |
| `UInt32` | AuthorSkin | The ID of the skin cosmetic of the author who sent the message |
| `UInt8` | AuthorColorRed | How red to make the author appear |
| `UInt8` | AuthorColorGreen | How green to make the author appear |
| `Uint8` | AuthorColorBlue | How blue to make the author appear |
| `String` | MessageContent | The content of the message |
| `Boolean` | FromQuickChat | Whether or not this message was sent via the quick chat menu |