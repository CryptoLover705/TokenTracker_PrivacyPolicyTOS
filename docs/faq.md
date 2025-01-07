## `faq` Command

### Description:
This command displays a Frequently Asked Questions (FAQ) menu with a list of questions that users can select to view the corresponding answers. The FAQ content includes information about the **TokenTracker** bot, its features, and how to interact with the bot.

### Command Usage:
`/faq`

### Command Flow:

1. **Embed Creation:**
   - The bot creates an embed with a title "📖 Frequently Asked Questions" and a description inviting users to select a question from a dropdown menu to view the answer.
   - The embed footer contains the text: "Brought to you by TokenTracker", and the embed includes a timestamp.

2. **Dropdown Menu:**
   - The bot generates a selection menu with the FAQ questions, labeled `Q1: What is TokenTracker?`, `Q2: Do you have a Discord server?`, and so on.
   - The user can select a question to view its answer.

3. **Menu Interaction Handling:**
   - The bot sets up a collector to handle user interactions with the dropdown menu.
   - If the user interacts with the menu, the bot checks if the interaction is from the user who originally invoked the command.
   - Once a valid selection is made, the bot responds with an embed containing the answer to the selected question.

4. **Update the Embed:**
   - Upon selection, the bot updates the original embed with the corresponding answer and keeps the selection menu.
   - The bot displays the answer to the user, along with the question's reference number (e.g., "Answer to Q1").

5. **Timeout and Component Removal:**
   - The bot sets a 1-minute timeout for the interaction collector.
   - After the collector ends, the selection menu is removed from the message, preventing further interactions.

6. **Error Handling:**
   - If any error occurs, such as during the creation of the FAQ embed or the selection handling, the bot will reply with an error message and log the issue.

### Example Usage:
```bash
/faq
```
