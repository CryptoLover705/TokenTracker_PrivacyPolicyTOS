## `deletepricechannels` Command

### Description:
This command allows users with the **Manage Server** permission to delete the price channels and category created for tracked tokens in the server. It also removes the corresponding data from the database.

### Command Usage:
`/deletepricechannels`

### Command Flow:

1. **Permission Check:**
   - The command is restricted to users with the **Manage Server** (`ManageGuild`) permission. If the user lacks this permission, the bot will respond with an error message indicating the lack of required permissions.

2. **Defer Reply:**
   - The bot will defer the reply to give time for processing while deleting the price channels. This prevents timeouts during the execution of the command.

3. **Database Operations:**
   - The bot connects to the database and fetches all price channels associated with the current guild.
   - If no price channels are found in the database, a message is sent notifying the user that no price channels exist.

4. **Delete Price Channels:**
   - For each price channel found in the database, the bot will attempt to delete the channel from Discord. If the channel exists, it will be deleted.
   - After deleting each price channel, the corresponding database entry will also be removed.

5. **Delete "Tracked Price" Category:**
   - The bot checks if the "Tracked Price" category still contains any channels. If the category is empty, it will be deleted.

6. **Completion Message:**
   - Once the price channels and category have been successfully deleted, the bot will notify the user with a message confirming the deletion.
   - If an error occurs during the process, an error message will be sent, indicating that the deletion was unsuccessful.

### Permissions:
- **Manage Server:** This command requires the **Manage Server** permission to be used. Users without this permission will receive an error message and the command will not proceed.

### Example Usage:
```bash
/deletepricechannels
```
