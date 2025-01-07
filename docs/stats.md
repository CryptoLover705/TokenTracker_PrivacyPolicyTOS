## `stats` Command

### Description:
This command provides detailed statistics about the bot, including information about tracked tokens, guilds, system performance, and bot uptime. It also includes data about the bot's memory and CPU usage, and offers insight into the most tracked tokens and networks.

### Command Usage:
`/stats`

- No parameters required.

### Command Flow:

1. **Permission Check:**
   - This command can be used by any user in the guild where the bot is deployed. No special permissions are required to execute the command.

2. **Database Operations:**
   - The bot fetches data from the database using the `getDatabase` utility.
   - It retrieves the following:
     - The total number of unique tokens being tracked.
     - The total number of guilds and the number of guilds tracking tokens.
     - The most tracked token, along with the network it belongs to.
     - The total number of records and price alerts in the database.

3. **System Metrics:**
   - The bot collects system-level metrics using the `os` module, including:
     - Memory usage (total and free).
     - CPU model and the number of CPU cores.
     - System uptime (in days and hours).

4. **Bot Metrics:**
   - The bot collects the following:
     - Uptime (formatted as days, hours, minutes, and seconds).
     - Total number of commands and active users, channels, and roles.
     - Average number of tracked tokens per guild.

5. **Advanced Token Stats:**
   - The bot aggregates data for tokens by network to identify the most tracked network.

6. **Embed Construction:**
   - The bot builds an embed message with all the gathered statistics.
   - The embed includes information like:
     - Total tokens tracked, networks tracked, and the most tracked token.
     - Bot and system uptime, CPU info, memory stats, and command usage.

7. **Final Reply:**
   - The bot sends an embedded message containing the statistics to the channel where the command was invoked.
   - If an error occurs, an error message is sent to the user.

### Permissions:
- **No specific permissions** are required to use this command. Any user in the guild can execute it.

### Example Usage:
```bash
/stats
```
