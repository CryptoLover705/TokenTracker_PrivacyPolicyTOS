## `suggesttoken` Command

### Description:
This command allows users to suggest a new token for tracking by providing a token address and network. The suggestion is validated and recorded in the database, and an acknowledgment message is sent to the user. The suggestion is also logged in the main bot server, where it can be voted on by community members.

### Command Usage:
`/suggesttoken <token_address> <network>`

- **token_address** (required): The address of the token you want to suggest.
- **network** (optional): The network the token is on. Defaults to `eth` (Ethereum) if not specified. Supported networks include: `eth`, `bsc`, `polygon_pos`, `solana`, `base`, and `tron`.

### Command Flow:

1. **Input Validation:**
   - The command checks that the token address is valid for the specified network.
   - Supported networks:
     - Ethereum (`eth`), Binance Smart Chain (`bsc`), Polygon (`polygon_pos`), Base, and Tron.
     - Each network has its own address format validation pattern.
   - If the network is unsupported or the address format is invalid, an error message is returned to the user.

2. **Token Data Fetching:**
   - The bot attempts to fetch the token's name and symbol from the GeckoTerminal API using the provided address and network.
   - If the API request fails, it falls back to using 'Unknown' as the token's name and symbol.

3. **Logging the Suggestion:**
   - The suggestion (including user details, token address, network, and fetched data) is logged into the `suggestedTokens` collection in the bot's database.
   - The suggestion includes the user ID, username, guild ID, and the token's details.

4. **Sending Acknowledgment:**
   - An acknowledgment message is sent to the user, confirming the suggestion and displaying the token's name and symbol.

5. **Logging in Main Server:**
   - The suggestion is sent to a designated suggestion log channel in the main bot server.
   - The message includes the user's information, guild details, and the token's data.
   - Two reactions (`✅` and `❌`) are added to the suggestion message to allow voting on whether to track the token.

6. **Error Handling:**
   - If any errors occur during the execution of the command, an error message is sent to the user.

### Permissions:
- **No specific permissions** are required to use this command. Any user in the guild can execute it.

### Example Usage:
```bash
/suggesttoken 0x1234567890abcdef1234567890abcdef12345678 eth
```
