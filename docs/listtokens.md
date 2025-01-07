### `listtokens` Command

#### Description:
This command displays all tokens being tracked in the current server, grouped by the channel where updates are sent for each token.

#### Command Flow:

1. **Fetch Tracked Tokens:**
   - The bot queries the `trackedTokens` collection in the MongoDB database to fetch tokens being tracked in the current guild (server).
   - It uses the `guildId` field to filter tokens for the current guild.

2. **Permission Check:**
   - The bot assumes that the user has permission to run the command without any explicit permission check in this case, but you can add permissions if necessary.

3. **Fetch Token Data from GeckoTerminal:**
   - For each tracked token, the bot fetches data such as the token's name, symbol, address, and network from the GeckoTerminal API.
   - If the data fetch fails, the bot logs the error and includes the token with basic information.

4. **Group Tokens by Channel:**
   - The tokens are grouped by the channel ID where the price updates are being sent.
   - The bot then formats the tokens by displaying the channel name, token name, symbol, address, and network.

5. **Pagination Setup:**
   - The bot uses pagination to show the tokens in multiple pages if necessary.
   - The number of tokens per page is set to 1 (you can adjust this if needed).
   - The total number of pages is calculated based on the number of tokens.

6. **Embed Generation:**
   - The bot generates an embed for each page that lists the tokens for a specific channel.
   - It also includes a footer indicating the current page and the total number of tokens.

7. **Navigation Buttons:**
   - The bot generates two buttons, "⬅️" and "➡️", to allow users to navigate between pages of tokens.
   - These buttons are disabled when the user is on the first or last page.

8. **Message Collector:**
   - The bot listens for button interactions to handle pagination.
   - If the user interacts with the buttons, the bot updates the embed and buttons accordingly.

9. **Timeout:**
   - If no interaction occurs within 60 seconds, the buttons are removed, and a timeout message is sent.

#### Example Response:

- If there are tokens being tracked, the bot might reply with an embed that lists the tokens grouped by channel, like so:
    ```
    Tracked Tokens in This Server

    **Channel: general (ID: 123456789012345678)**
    **TokenName (SYM)** - Address: **0xABC123...** 
    Network: **Ethereum**

    Page 1 of 3 | Total Tokens: 10
    ```

- If no tokens are being tracked, the bot will reply with:
    ```
    No tokens are being tracked in this server.
    ```
