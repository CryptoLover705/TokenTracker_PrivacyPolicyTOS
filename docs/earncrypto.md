## `earncrypto` Command

### Description:
This command displays a list of crypto faucet links with pagination. It reads the faucet links from a `faucets.txt` file and presents them to the user in an embedded message with navigation buttons.

### Command Usage:
`/earncrypto`

### Command Flow:

1. **Reading Faucet Data:**
   - The bot reads the `faucets.txt` file, which contains faucet names and links in the format `name | link`.
   - If the file cannot be read, the bot will notify the user with an error message.

2. **Faucet Data Parsing:**
   - Each line in the file is split by a pipe (`|`), and the name and link are extracted.
   - The parsed data is stored as an array of objects with `name` and `link` properties.

3. **Pagination:**
   - The command paginates the faucet links, displaying 20 links per page.
   - **Navigation Buttons**: The bot adds "⬅️ Previous" and "Next ➡️" buttons to allow users to navigate between pages of links.
     - If the user is on the first page, the "Previous" button is disabled.
     - If the user is on the last page, the "Next" button is disabled.

4. **Embed Creation:**
   - The bot creates an embedded message for the current page of faucet links, with the faucet names displayed as clickable links.
   - The embed footer includes the current page and the total number of pages.
   - If there are no more faucet links to display, a message indicating this will be shown.

5. **Sending the Embed:**
   - The embed is sent as a message with the pagination buttons.
   - The bot uses a message collector to listen for button interactions and update the embed accordingly.

6. **Error Handling:**
   - If there is an error reading the `faucets.txt` file or processing the pagination, an error message is sent to notify the user of the issue.

### Example Usage:
```bash
/earncrypto
```
