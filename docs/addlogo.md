## `addlogo` Command

### Description:
This command allows the bot owner to add or update a logo for a specified token. The logo can either be uploaded as an image file or provided through a URL.

### Command Usage:
`/addlogo token_address=<token_address> logo_url=<logo_url> logo=<logo_attachment>`

- `token_address` (required): The address of the token for which the logo is being added.
- `logo_url` (optional): A valid URL pointing to the logo image.
- `logo` (optional): An image attachment that will be used as the logo.

### Command Flow:

1. **Permission Check:**
   - Only the bot owner (identified by `BOT_OWNER_ID` in the `.env` file) is allowed to use this command. 
   - If the user isn't the bot owner, a permission error message is sent.

2. **Guild Check:**
   - This command is restricted to be used in the main bot server, identified by `GUILD_ID` in the `.env` file.
   - If the command is used outside of the main server, an error message is returned.

3. **Parameter Validation:**
   - The user must provide a valid `token_address` as an argument.
   - The user must provide either a logo image URL (`logo_url`) or an image attachment (`logo`).
   - The `logo_url` or `logo_attachment` must be a valid URL that starts with `http://` or `https://`.

4. **Database Operations:**
   - The command accesses the database using the `getDatabase` utility and checks if the provided token address is already being tracked.
   - If the token is not found in the tracked tokens list, a follow-up message informs the user that the token is not being tracked in the main server, but the logo will still be added.
   - The logo URL is stored or updated in the database for the given token address. The `upsert` option ensures that if the token does not exist, it will be added.

5. **Final Reply:**
   - Once the logo has been successfully added or updated, a success message is sent.
   - If an error occurs at any point, an error message is returned indicating the failure.

### Permissions:
- **Bot Owner Only:** The command can only be used by the bot owner, as indicated by the `BOT_OWNER_ID` in the `.env` file.
- **Main Server Only:** The command can only be used in the specified main bot server (`GUILD_ID`).

### Example Usage:
```bash
/addlogo token_address=0x123456789abcdef logo_url=https://example.com/logo.png
```

Or, if using an attachment:
```bash
/addlogo token_address=0x123456789abcdef logo=@logo.png
```
