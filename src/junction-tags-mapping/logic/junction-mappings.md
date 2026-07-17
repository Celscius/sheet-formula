# Junction Table Mapping Logic

This function automatically builds a strict relational database junction table by parsing a comma-separated list of strings and mapping them to dynamic row IDs.

## Expected Input Data Shape
The formula expects a table (`Items`) containing an explicit primary key and a text column of tags:
* `item_id`: Integer (Unique)
* `tags`: String (Comma + space separated, e.g., "dev, auth")

## The Formula
```excel
=LET(
  items, FILTER(Items!A2:B, Items!A2:A<>""),
  tags, FILTER({ROW(Tags!A2:A), Tags!A2:A}, Tags!A2:A<>""),
  ...
)
```

## Step-by-Step Breakdown
1. **`items` variable**: Grabs all rows from the main sheet while skipping empty rows.
2. **`tags` variable**: Pairs the spreadsheet row number (acting as our `tag_id`) with the text name.
3. **`SPLIT` & `MAP`**: Loops through each comma-separated string, breaks them apart, and uses `XLOOKUP` to find the matching ID.
4. **`VSTACK`**: Combines all individual mappings into a final, multi-row table.

## Expected Output Data Shape
Generates a two-column array ready for SQL import:
* `item_id` (Foreign Key to Items)
* `tag_id` (Foreign Key to Tags)
