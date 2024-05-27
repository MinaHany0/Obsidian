## Array Representation vs List Representation
### Array Representation
``` mermaid
graph TD
A --> B
A --> C
B --> D
B --> E
C --> F
C --> G
```

you can form an array with elements in this order 
	`A , B , C , D , E , F , G , H`

where properties are

| Node | index | Left Child | Right Child |
| ---- | ----- | ---------- | ----------- |
| A    | 1     | 2          | 3           |
| B    | 2     | 4          | 5           |
| C    | 3     | 6          | 7           |
Notice that the children of node are always indexed = 2n& 2n+1


