```
=LET(
  items, FILTER(Items!A2:B, Items!A2:A<>""),
  tags, FILTER({ROW(Tags!A2:A), Tags!A2:A}, Tags!A2:A<>""),
  
  REDUCE(
    {"item_id", "tag_id"}, 
    SEQUENCE(ROWS(items)), 
    LAMBDA(acc, idx,
      LET(
        itemId, INDEX(items, idx, 1),
        tagString, INDEX(Items!C2:C, idx),
        tagList, SPLIT(tagString, ", "),
        
        mapped, MAP(tagList, LAMBDA(t, 
          {itemId, XLOOKUP(t, CHOOSECOLS(tags, 2), CHOOSECOLS(tags, 1))}
        )),
        
        VSTACK(acc, mapped)
      )
    )
  )
)

```
