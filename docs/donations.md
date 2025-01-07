## `donate` Command

### Description:
This command displays the donation options for supporting the **TokenTracker** bot. It provides users with cryptocurrency wallet addresses and additional ways to contribute to the project.

### Command Usage:
`/donate`

### Command Flow:

1. **Embed Creation:**
   - The bot builds an embedded message to display the donation options with a green color (`#00AE86`).
   - The title of the embed is "💖 Support TokenTracker", and the description contains:
     - A message thanking users for their support.
     - **Crypto Wallets**: Multiple cryptocurrency wallet addresses for donations (Ethereum, Bitcoin, Dogecoin, Litecoin, Tron).
     - An option to tip the bot owner through a specified platform.

2. **Bot Owner ID:**
   - The bot fetches the **Bot Owner ID** from the `.env` file, which is used to create a mention of the owner for additional donation instructions.

3. **Footer and Timestamp:**
   - The embed footer contains the text: "TokenTracker - Powered by your generosity".
   - The embed includes a timestamp of when the message was sent.

4. **Sending the Embed:**
   - The bot sends the embed in the channel where the command was invoked, making the donation options visible to the user.
   - The command does not need to be ephemeral, so the message is visible to everyone in the channel.

5. **Error Handling:**
   - If an error occurs while processing the command, an error message is sent to notify the user of the issue.

### Example Usage:
```bash
/donate
```
