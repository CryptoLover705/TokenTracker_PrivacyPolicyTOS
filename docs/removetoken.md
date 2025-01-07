### `removetoken` Command

#### Description:
This command allows users (with the appropriate permissions) to remove a tracked token from the database, effectively stopping the bot from tracking that token in the specified guild.

#### Command Flow:

1. **Permission Check:**
   - The bot checks if the user has the `Manage Server` permission before proceeding. If the user lacks this permission, the bot responds with an error message indicating the need for the required permission.

2. **Token Removal:**
   - The bot retrieves the `token_address` from the interaction options (it assumes the token address is passed as an argument).
   - It queries the `trackedTokens` collection in the database to find and remove the document that matches the guild ID and the token address.
   - If the token is successfully removed, the bot responds with a success message confirming the removal.
   - If the token is not found in the tracked list, the bot informs the user that the token is not being tracked.

3. **Error Handling:**
   - If an error occurs during the execution of the command (e.g., database connection issues), the bot catches the error and sends a generic error message.

#### Example Interactions:

- **Success Case (Token Removed):**
    ```
    Successfully removed token: **0x123abc...**
    ```

- **Failure Case (Token Not Found):**
    ```
    Token **0x123abc...** not found in the tracked list.
    ```

- **Error Handling:**
    ```
    An error occurred while trying to remove the token. Please try again later.
    ```

#### Notes:
- **Permission Enforcement:** The command requires the user to have the `Manage Server` permission to ensure that only authorized users can remove tokens from the tracked list.
- **Database Query:** The bot uses the `deleteOne` method to remove a single document (token) from the `trackedTokens` collection based on the guild ID and token address.
- **Ephemeral Replies:** The command uses ephemeral replies for error handling to ensure that only the user invoking the command sees the error messages, maintaining privacy and reducing clutter in the channel.
