## `globaltokens` Command

### Description:
This command displays all tokens that are being tracked globally across all servers, grouped by server. The command is accessible only by the bot owner.

### Command Usage:
`/globaltokens`

### Command Flow:

1. **Permission Check:**
   - The bot verifies if the user invoking the command is the bot owner by comparing their user ID with the `BOT_OWNER_ID` environment variable.
   - If the user is not the bot owner, it sends an ephemeral message saying they do not have permission to use the command.

2. **Database Query:**
   - The bot retrieves all tracked tokens from the database (`trackedTokens` collection), grouped by guild ID.

3. **Fetching Token Data:**
   - For each guild, the bot fetches the token data for each tracked token using the GeckoTerminal API (`https://api.geckoterminal.com/api/v2/networks/{network}/tokens/{tokenAddress}`).
   - If the token data is successfully fetched, the bot extracts the token's name and symbol and stores them.
   - If fetching token data fails, the bot logs an error and includes a fallback message in the list of tokens for the guild.

4. **Token Grouping by Guild:**
   - The bot groups tokens by server and creates a formatted string showing the guild’s name, the token’s name, symbol, and the network it’s on.

5. **Pagination:**
   - The tokens are displayed with pagination, showing a fixed number of guilds per page (1 guild per page in this case). The total number of pages is calculated based on the total number of tracked guilds.
   - The user can navigate between pages using "previous" and "next" buttons.

6. **Embed Generation:**
   - The `generateEmbed` function creates a paginated embed message containing the tracked tokens for the current page.
   - The `generateButtons` function creates navigation buttons to allow the user to switch between pages.

7. **Button Interaction:**
   - The bot listens for button interactions (prev/next) and updates the message with the appropriate page of tokens.
   - If the user who clicked the button is not the one who invoked the command, they are informed that only the command invoker can interact with the buttons.

8. **Timeout Handling:**
   - If the button collector times out (after 60 seconds), the buttons are removed, and the bot informs the user that the navigation has timed out.

9. **Error Handling:**
   - If any error occurs while fetching or processing the data, the bot catches the error and sends an error message, either to the original interaction or a follow-up message.

### Example Usage:
```bash
/globaltokens
```
