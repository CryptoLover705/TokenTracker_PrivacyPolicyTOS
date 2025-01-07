## `tracktoken` Command

### Description:
This command allows users to start tracking a token on a specific network within a selected channel. It checks for the necessary permissions, validates the token address and network, ensures the token exists on the selected network, and logs the token in the database if not already tracked.

### Command Usage:
`/tracktoken <token_address> <network> <channel>`

- **token_address** (required): The address of the token to be tracked.
- **network** (optional): The network the token is on. Defaults to `eth` (Ethereum) if not specified. Supported networks include: `eth`, `bsc`, `polygon_pos`, `solana`, `base`, and `tron`.
- **channel** (optional): The channel where token updates will be sent. If not specified, the current channel is used.

### Command Flow:

1. **Permission Validation:**
   - The command checks if the user has the **Manage Guild** permission. If not, an error message is returned.

2. **Input Validation:**
   - The token address and network are validated to ensure they match the correct format for the selected network.
   - Supported network address formats are validated using regular expressions.

3. **Token Existence Check:**
   - The bot checks if the token exists on the selected network by making a request to the GeckoTerminal API.
   - If the token does not exist on the network, the bot checks if it exists on any other supported networks and informs the user accordingly.

4. **Database Check:**
   - The command checks if the token is already being tracked in the specified guild. If the token is already tracked, an error message is sent.

5. **Token Tracking:**
   - If the token is not already tracked, the bot adds the token to the `trackedTokens` collection in the database, associating it with the guild, token address, network, and channel.

6. **Reply Message:**
   - The bot sends a success message confirming that the token is being tracked in the specified channel.

7. **Error Handling:**
   - If an error occurs at any step, the bot catches the error and sends an error message to the user.

### Permissions:
- **Manage Guild** permission is required to use this command.

### Example Usage:
```bash
/tracktoken 0x1234567890abcdef1234567890abcdef12345678 eth #crypto-updates
```
