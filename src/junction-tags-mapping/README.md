# Google Sheets SQL-Style Tagging Prototype

A prototype demonstrating how to handle random, on-the-fly user tagging in a spreadsheet while automatically generating a strict, relational 3-table SQL structure (Items, Tags, Junction) using modern Google Sheets formulas.

## The Architecture
Instead of managing three sheets manually, this project utilizes `LET`, `MAP`, and `LAMBDA` to auto-generate database mapping tables from a simple, human-readable comma-separated list.

### Input (Items Sheet)

| item_id | name             | tags              |
|---------|------------------|-------------------|
| 1       | Build Login Page | dev, auth, urgent |

### Auto-Generated Outputs
1. **Tags Sheet**: Extracts unique strings and assigns explicit row-ID logic.
2. **Junction Sheet**: Maps `item_id` directly to the dynamically generated `tag_id`.

## project structure
```
├── README.md          # Project overview & quick start
├── data/
│   ├── items.csv      # Sample input data (Item Name, Comma Tags)
│   ├── tags.csv       # Expected Master Tags output
│   └── junction.csv   # Expected Junction Table output
└── formulas/
    ├── master_tags.md # Clean, multi-line Master Tag formula with explanations
    └── junction_map.md# Clean, multi-line Junction formula with step-by-step breakdown

```
