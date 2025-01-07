## `edittoken` Command

### Description:
This command allows users with the **Manage Server** permission to edit the details of a tracked token in the current server. It lets users select a token and then choose which field (token address, network, or channel) to edit.

### Command Usage:
`/edittoken`

### Command Flow:

1. **Permission Check:**
   - The bot checks if the user has the **Manage Server** permission (`MANAGE_GUILD`).
   - If the user does not have the required permission, an error message is sent.

2. **Fetch Tracked Tokens:**
   - The bot fetches all tokens tracked in the current server from the database.
   - If no tokens are tracked, the bot will notify the user.

3. **Token Selection:**
   - The bot creates a dropdown menu for the user to select a token to edit from the list of tracked tokens.
   - Each token is represented by its **token address** and **network**.

4. **Field Selection:**
   - After selecting a token, the bot prompts the user to select which field of the token they want to edit:
     - **Token Address**
     - **Network**
     - **Channel**

5. **Editing the Field:**
   - Depending on the field selected, the bot prompts the user to enter the new value for the field:
     - For **Token Address**, the bot updates the token address.
     - For **Network**, the bot updates the network (converted to lowercase).
     - For **Channel**, the bot asks for a valid channel ID (must be a valid mention).

6. **Updating the Token:**
   - After the user provides the new value, the bot validates it and updates the token details in the database.
   - A confirmation message is sent to notify the user of the successful update.

7. **Error Handling:**
   - If any errors occur during the process, such as invalid input or a failure to update the token, an error message is sent.

### Example Usage:
```bash
/edittoken
```
