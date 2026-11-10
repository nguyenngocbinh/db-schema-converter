# DB Schema Converter

VS Code extension for extracting table metadata from IBM Db2 or Microsoft SQL Server and generating editable DDL for the opposite engine.

## Scope (0.1.0)

- Connect to IBM Db2 or SQL Server as a source.
- Browse schemas and tables.
- Read columns, types, length/precision/scale, nullability, defaults and identity.
- Read primary keys, unique constraints, foreign keys and regular indexes.
- Generate CREATE TABLE, ALTER TABLE ADD CONSTRAINT and CREATE INDEX.
- Preview and edit generated SQL in the extension.
- Save edited SQL to a .sql file.
- SQL is not executed by the extension.

## Build

Requirements: Node.js 20 LTS, VS Code 1.85+, and network access to the database.

```powershell
npm install
npm run compile
npx vsce package
```

Install the generated VSIX using Extensions: Install from VSIX..., then run **DB Schema Converter: Open**.

## Drivers

- SQL Server: `mssql`.
- Db2: `ibm_db`. Windows native Db2 CLI/driver prerequisites may be required; validate on the target machine.

## Limitations

- Metadata SQL targets Db2 LUW `SYSCAT` and SQL Server `sys.*`. Db2 z/OS or IBM i need another adapter.
- Foreign-key referential actions are warned, not automatically translated.
- Computed column expressions are not extracted.
- Db2 index extraction supports regular indexes only.
- SQL Server `NCHAR`/`NVARCHAR` lengths are normalized from catalog bytes to characters. Review generated lengths.
- Db2 catalog length semantics can vary by type; review graphic and LOB mappings.
- Referenced tables must exist before applying FK statements.
- Unknown mappings produce warnings and placeholder SQL. Review all generated SQL before use.

## Security

Credentials are kept in extension-host memory for the active panel session and are not persisted. Use least-privilege read-only accounts. Never commit connection strings, passwords, or customer data.

Repository: https://github.com/nguyenngocbinh/db-schema-converter
