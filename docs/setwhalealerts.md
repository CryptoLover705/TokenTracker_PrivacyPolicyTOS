## `setwhalealerts` Command

### Description:
This command allows the server administrators to set up whale alert notifications for tokens being tracked by the bot. It sends alerts when a token's transaction surpasses a specified threshold. Alerts can be configured for a specific channel and a role can be mentioned when an alert is triggered.

### Command Usage:
`/setwhalealerts threshold=<threshold> channel=<channel> mention_role=<mention_role>`

- `threshold` (required): The transaction amount in USD that will trigger the whale alert.
- `channel` (required): The text channel where the whale alerts will be sent.
- `mention_role` (optional): The role that will be mentioned in the alert message when a whale transaction occurs.

### Command Flow:

1. **Permission Check:**
   - Only users with the `Manage Guild` permission are allowed to use this command.
   - If the user does not have the required permission, a permission error message is sent.

2. **Guild Check:**
   - This command works within the guild where the bot is deployed.
   - The bot checks if any tokens are being tracked in the server. If no tokens are found, an error message is sent.

3. **Token Selection:**
   - If only one token is tracked, the bot automatically proceeds with that token. If multiple tokens are tracked, the user must select which token to set the whale alert for. The bot asks the user to choose a token by replying with a number.

4. **Threshold Validation:**
   - The user must provide a `threshold` value that meets a minimum value, which is $100,000. If the provided value is below this threshold, the bot sends a message informing the user of the required minimum.

5. **Channel and Permissions Validation:**
   - The user must select a valid text channel for whale alerts.
   - The bot checks if it has permission to send messages in the selected channel. If the bot lacks permission, an error message is sent.

6. **Database Operations:**
   - The bot retrieves information from the database to fetch the list of tracked tokens for the server.
   - If a whale alert is being set for an existing token, the bot updates the alert configuration in the database. If the token is not already in the database, it adds the new alert configuration.

7. **Final Reply:**
   - Once the whale alert configuration is successfully saved, the bot sends a confirmation message, displaying the token, threshold, and other settings in an embedded message.
   - If an error occurs during any part of the process, the bot sends a failure message.

### Permissions:
- **Manage Server:** The command can only be used by members with the `Manage Server` permission in the server.

### Example Usage:
```bash
/setwhalealerts threshold=500000 channel=#whale-alerts mention_role=@WhaleAlertRole
```
