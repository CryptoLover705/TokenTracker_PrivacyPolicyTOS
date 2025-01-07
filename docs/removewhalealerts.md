### `removewhalealert` Command

#### Description:
This command allows users with the required permissions to remove an existing whale alert for a specific token in the current server. The whale alert contains a threshold for big transactions involving the token, as well as the channel to send the alerts and any role to mention.

#### Command Flow:

1. **Permission Check:**
   - The bot checks if the user has the `Manage Server` permission. If the user does not have this permission, the bot replies with an error message indicating that the `Manage Server` permission is required to use the command.

2. **Token Address and Database Query:**
   - The bot retrieves the `token_address` from the options passed by the user in the interaction.
   - It queries the `whaleAlerts` collection in the database to find an alert for the given `token_address` in the current guild.

3. **Alert Removal:**
   - If a matching whale alert is found, the bot proceeds to remove it from the database using the `deleteOne` method, and it sends a confirmation message indicating the successful removal of the alert.
   - If no alert is found for the provided token address, the bot notifies the user that no whale alert was configured for the specified token.

4. **Error Handling:**
   - If an error occurs during execution (such as a database connection issue or incorrect data), the bot catches the error and responds with a generic message to inform the user.

#### Example Interactions:

- **Success Case (Whale Alert Removed):**
    ```
    Whale alert for token **TokenName (TSYM)** has been successfully removed.
    ```

- **Failure Case (No Whale Alert Found):**
    ```
    No whale alert found for token address **0x123abc...** in this server.
    ```

- **Error Handling:**
    ```
    An error occurred while removing the whale alert. Please try again later.
    ```

#### Notes:
- **Permission Enforcement:** The command ensures that only users with the `Manage Server` permission can remove whale alerts, which prevents unauthorized users from modifying the alert settings.
- **Database Query:** The bot checks the `whaleAlerts` collection for an existing alert for the given token address. If found, it is deleted from the database. The response includes both the token name and symbol to make the alert's identity clear to the user.
- **Ephemeral Replies:** The command uses ephemeral replies for error handling, ensuring that only the user who invoked the command sees the error messages.
