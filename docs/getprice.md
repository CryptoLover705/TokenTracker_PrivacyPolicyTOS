## `getprice` Command

### Description:
This command fetches the current prices of all tokens being tracked in the server. It retrieves token price data from the GeckoTerminal API and presents the prices of the tokens in an easily readable format.

### Command Usage:
`/getprice`

### Command Flow:

1. **Initial Setup:**
   - The bot defers the reply to handle delays while processing the command (`await interaction.deferReply()`).
   - The guild ID is retrieved from the interaction context (`guildId`).
   - The database connection is established using the `getDatabase` function, and the `trackedTokens` collection is queried for tokens tracked in the guild.

2. **Check for Tracked Tokens:**
   - The bot checks if there are any tokens tracked in the server. If no tokens are found, the bot replies with a message saying "No tokens are currently being tracked in this server."

3. **Fetch Token Data:**
   - For each token in the guild's tracked tokens:
     - The bot makes a request to the GeckoTerminal API to fetch the token’s data, including its name and symbol.
     - The bot then uses the `getTokenData` function to fetch pool data for the token from the network.
     - If there are pools available for the token, the bot selects the pool with the highest liquidity (reserve in USD) and fetches the token's price from this pool.
     - If no pools are available or price data is missing, the bot provides a message indicating the issue.

4. **Price Messages:**
   - The bot constructs a message for each tracked token, displaying the token’s name, symbol, network, and its current price (or an appropriate error message if the price is unavailable).

5. **Reply to User:**
   - If there are price messages for the tracked tokens, the bot replies with the list of token prices.
   - If there were no valid prices found or an error occurred, the bot informs the user that it failed to fetch prices.

6. **Error Handling:**
   - If any error occurs during the command execution (such as an issue with fetching token data), the bot logs the error and replies with a generic error message to the user.
   - If the bot had already replied or deferred the interaction, it follows up with an error message in a private response.

### Example Usage:
```bash
/getprice
```
