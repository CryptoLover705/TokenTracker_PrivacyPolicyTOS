## `trackanalytics` Command

### Description:
This command fetches token analytics from GeckoTerminal based on a given token address and network. It validates the token address and network, retrieves analytics data (such as token price, volume, FDV, and more), and displays it in a paginated embed format. The user can navigate between pages of token pool information using the "Next" and "Previous" buttons.

### Command Usage:
`/trackanalytics <token_address> <network>`

- **token_address** (required): The address of the token you want to fetch analytics for.
- **network** (optional): The network the token is on. Defaults to `eth` (Ethereum) if not specified. Supported networks include: `eth`, `bsc`, `polygon_pos`, `solana`, `base`, and `tron`.

### Command Flow:

1. **Input Validation:**
   - The command checks that the token address is valid for the specified network.
   - Supported networks:
     - Ethereum (`eth`), Binance Smart Chain (`bsc`), Polygon (`polygon_pos`), Solana (`solana`), Base (`base`), and Tron (`tron`).
     - Each network has its own address format validation pattern.
   - If the network is unsupported or the address format is invalid, an error message is returned to the user.

2. **Token Validity Check:**
   - The bot checks whether the token exists on the selected network by calling the GeckoTerminal API.
   - If the token is invalid for the selected network, the bot suggests valid networks where the token might exist.

3. **Token Data Fetching:**
   - The bot retrieves the token's name, symbol, and analytics data (such as price, volume, FDV) from GeckoTerminal.
   - If no valid pools are found or data retrieval fails, the bot informs the user.

4. **Embed Creation:**
   - An embed is created for each valid token pool, showing relevant analytics like the current price, volume, FDV, price change percentage, and more.
   - The embed contains a clickable link to the pool on GeckoTerminal for more information.

5. **Pagination:**
   - If multiple token pools exist, the bot divides the embed pages and implements pagination using "Next" and "Previous" buttons.
   - The user can navigate between pages by interacting with the buttons.

6. **Error Handling:**
   - If any errors occur during the execution of the command (e.g., failure to fetch data from the API), an error message is sent to the user.

### Permissions:
- **No specific permissions** are required to use this command. Any user in the guild can execute it.

### Example Usage:
```bash
/trackanalytics 0x1234567890abcdef1234567890abcdef12345678 eth
```
