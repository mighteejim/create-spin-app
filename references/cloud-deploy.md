# Fermyon Cloud Deploy

## Command

`spin cloud deploy --build`

## Notes

Run from the app directory containing `spin.toml`.

Interactive prompts:
- If the app declares `sqlite_databases`, deploy will ask to link or create a database.
- Default choice: create a new database and link it to the app, unless the user specifies an existing DB.
- When prompted for a DB name, accept the default unless the user asks for a specific name.

Output:
- Capture the app URL from deploy output and report it back.
