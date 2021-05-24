
Cosmetic Entry format:

|    Type   |      Name     |      Description       |
|-----------|---------------|------------------------|
| `UInt8`   | Cosmetic Type | The cosmetic type      |
| `UInt8`   | Data Length   | The length of the data |
| `UInt8[]` | Data          | The cosmetic data      |

Cosmetic Types:

- Cosmetic Type 0 (PlayerColor). Data is 4 UInt8s for RGBA
