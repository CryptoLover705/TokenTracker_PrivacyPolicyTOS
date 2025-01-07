### `listpricechannels` Command

#### Description:
This command lists all the channels where the prices for tracked tokens are displayed in the current guild.

#### Command Flow:

1. **Permission Check:**
   - The command first checks if the user who invoked it has the "Manage Server" (`ManageGuild`) permission. If not, the bot will respond with a permission error.

2. **Defer Reply:**
   - The command uses `interaction.deferReply()` to ensure the bot doesn't time out while processing the request.

3. **Fetch Price Channels Data:**
   - The bot connects to the MongoDB database and queries the `priceChannels` collection to retrieve all price channels associated with the guild.

4. **Check for Price Channels:**
   - If no price channels are found in the database for the guild, the bot will inform the user that no price channels exist.

5. **Format and Send the List:**
   - If price channels are found, the bot formats them into a list, showing the token's symbol and the corresponding price channel, and sends this list as a reply.

6. **Error Handling:**
   - If any error occurs during the execution of the command, the bot catches it and replies with a generic error message.

#### Example Response:

If the bot successfully finds price channels, the response might look like:

```
Here are the price channels for tracked tokens:

**TOKEN_SYMBOL_1** - <#123456789012345678>
**TOKEN_SYMBOL_2** - <#987654321098765432>
```

If no price channels exist, the bot will reply with:

```
No price channels exist for tracked tokens in this guild.
```

#### Permissions:
- The command requires the `Manage Server` permission (`ManageGuild`) to be used by the invoking user.
