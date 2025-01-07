### `listwhalealerts` Command

#### Description:
This command displays a list of all whale alerts that have been configured in the current server. It provides details on each alert, including the token, threshold, channel, and the role (if any) that is mentioned when an alert is triggered.

#### Command Flow:

1. **Fetch Whale Alerts:**
   - The bot connects to the MongoDB database and queries the `whaleAlerts` collection to retrieve alerts configured for the current guild (`guildId`).
   - If no whale alerts exist for the guild, it responds with a message indicating there are no alerts.

2. **Embed Creation:**
   - If whale alerts exist, the bot constructs an embed to list the alerts.
   - The embed includes a title (`Whale Alerts Configured`), description (`Here is a list of all whale alerts configured for this server`), and a timestamp.

3. **Adding Fields to Embed:**
   - For each whale alert, the bot:
     - Converts the threshold value (USD amount) to a currency format (using `toLocaleString`).
     - Checks if a mention role is set and includes it in the alert details (if set).
     - Adds the token name, symbol, threshold, channel, and role information to the embed.

4. **Replying with Embed:**
   - The bot sends the embed containing the list of whale alerts as a reply to the user.

5. **Error Handling:**
   - If an error occurs while fetching whale alerts or sending the reply, the bot catches the error and responds with an error message.

#### Example Response:

- If whale alerts are configured, the bot will send an embed with a list of alerts like this:
    ```
    Whale Alerts Configured

    Here is a list of all whale alerts configured for this server:

    **TokenName (SYM)**
    **Threshold:** $100,000.00
    **Channel:** #whale-alerts
    **Mention Role:** @WhaleAlertRole
    ```

- If no whale alerts are configured, the bot will respond with:
    ```
    No whale alerts are currently configured for this server.
    ```

#### Notes:
- **Threshold Formatting:** The threshold value (USD) is displayed in a user-friendly format (e.g., `$100,000.00`).
- **Mention Role:** If a role has been set for alerts, it will appear as a mention (e.g., `@WhaleAlertRole`). If not, it will display 'None'.
- **Embed Structure:** The embed clearly organizes the whale alerts with token information, the alert threshold, associated channel, and mention role.
