The `sendfeedback` command allows users to submit feedback to the bot’s main server. The flow of this command ensures that feedback is properly submitted, and the user receives a response based on whether they are already in the bot’s main server.

### Key Functionality:

1. **User Check for Main Server:**
   - The command first checks if the user who issued the feedback command is a member of the bot's main server (using `GUILD_ID` from the `.env` file).
   - If the user is not in the main server, an invite link is generated to allow them to join. The invite is generated for a text-based channel where the bot has permission to create invites.

2. **Feedback Submission:**
   - If the user is in the main server, the bot collects the feedback text.
   - If no feedback is provided, the bot prompts the user to provide feedback.
   - The feedback is then formatted and sent as an embedded message to a specified channel in the main bot server (`channelId`).

3. **Reaction for Voting:**
   - Once the feedback is sent, the bot adds `✅` and `❌` reactions to the feedback message for voting purposes.

4. **Error Handling:**
   - If there is an issue with generating the invite link or submitting feedback (e.g., the specified channel does not exist or cannot send messages), appropriate error messages are sent to the user.

### Detailed Breakdown:

- **Step 1: User Verification in Main Server:**
  - The bot checks if the user is in the main server. If the user is not found, the bot generates an invite link.
  
- **Step 2: Feedback Collection:**
  - The bot checks if the user has provided feedback. If the feedback is missing, the bot asks the user to provide it.

- **Step 3: Embed Creation and Sending:**
  - Once the feedback is provided, the bot constructs an embedded message with the feedback text and user details. It sends this embedded feedback message to the designated channel in the main bot server.

- **Step 4: Reactions for Voting:**
  - The feedback message gets `✅` and `❌` reactions, allowing others to vote on the feedback.

### Example Interactions:

- **User Not in Main Server:**
  - If the user is not in the main server, they receive a message with an invite link:
    ```
    You are not in the bot's main server. Please join using the following invite link: [Join Server](invite_url)
    ```

- **Feedback Submitted Successfully:**
  - If the feedback is successfully submitted:
    ```
    Your feedback has been submitted and is now open for voting!
    ```

- **Error Handling (Feedback Channel Not Found):**
  - If the specified feedback channel does not exist or is unavailable:
    ```
    Could not find the feedback channel.
    ```

- **Error Handling (Invite Link Generation):**
  - If there is an error generating the invite link:
    ```
    There was an error generating the invite link. Please try again later.
    ```

### Suggestions for Improvements:
- **Feedback Channel ID:** Consider storing the feedback channel ID in a configuration file or the database instead of hardcoding it in the script for easier management.
- **Rate Limiting:** If the feedback submission system becomes heavily used, implementing rate limiting for the command could be a good idea to prevent spam submissions.
