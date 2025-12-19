# DiscordBot

Discord bot built with C# (.NET 9) and [Discord.Net](https://github.com/discord-net/Discord.Net).

## ✨ Features

- **Mention-based command handling**: Use `@BotName <command>` in Discord to interact
- **Automatic command registration**: All classes inheriting `BaseCommand` and decorated with `[DiscordCommand]` are auto-registered
- **Attribute-based permissions**: Use `[RequireGuildPermission]` and `[RequireChannelPermission]` to restrict commands
- **Built-in commands**:
  - `help` - Lists all available commands and their permissions
  - `about` - Shows bot information and uptime
  - `ping` - Replies with latency
  - `userinfo` - Shows information about a user
- **Configuration via `appsettings.json`**: Token, prefix, and more
- **Comprehensive logging**: Console logging for diagnostics and debugging
- **.NET 9 and C# 13**: Utilizes the latest language and runtime features

## 🚀 Getting Started

### Prerequisites

- [.NET 9 SDK](https://dotnet.microsoft.com/download)
- A Discord bot token ([How to create a bot](https://discord.com/developers/applications))

### Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/DiscordBot.git
   cd DiscordBot
   ```

2. **Configure the bot:**
   - Open `src/DiscordBot/appsettings.json`
   - Replace `"Token": "Key"` with your actual Discord bot token
   - Optionally set `"Prefix"` and `"GuildId"`

3. **Build and run:**
   ```bash
   dotnet build src/DiscordBot
   dotnet run --project src/DiscordBot
   ```

### Bot Permissions

Make sure your bot has the following permissions in your Discord server:
- Read Messages
- Send Messages
- Use Slash Commands (if applicable)
- Embed Links

## 📖 Usage

Mention the bot in any channel it has access to:

- `@BotName help` — Lists all commands and their permissions
- `@BotName about` — Shows bot info and uptime
- `@BotName ping` — Replies with latency
- `@BotName userinfo [@user]` — Shows info about a user (optional user parameter)

## 🔧 Extending the Bot

To add a new command:

1. Create a class inheriting from `BaseCommand` in the `Commands` folder
2. Decorate the class with `[DiscordCommand("yourcommand", "Description here")]`
3. (Optional) Add permission attributes:
   - `[RequireGuildPermission(GuildPermission.Administrator)]`
   - `[RequireChannelPermission(ChannelPermission.ManageMessages)]`
4. Implement the `ExecuteAsync(SocketMessage message, string[] args)` method

### Example Command

```csharp
[DiscordCommand("greet", "Greets the user")]
[RequireGuildPermission(GuildPermission.SendMessages)]
public class GreetCommand : BaseCommand
{
    public override async Task ExecuteAsync(SocketMessage message, string[] args)
    {
        var greeting = args.Length > 0 
            ? $"Hello, {string.Join(" ", args)}!" 
            : $"Hello, {message.Author.Username}!";
            
        await ReplyAsync(message, greeting);
    }
}
```

The bot will automatically discover and register your command at startup.

## ⚙️ Configuration

Example `appsettings.json`:

```json
{
  "Bot": {
    "Token": "YOUR_BOT_TOKEN",
    "Prefix": "!",
    "GuildId": 0
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Discord": "Warning"
    }
  }
}
```

### Configuration Options

- `Token`: Your Discord bot token (required)
- `Prefix`: Command prefix (optional, defaults to mention-only)
- `GuildId`: Specific guild ID for testing (0 for global commands)

## 🏗️ Project Structure

```
DiscordBot/
├── src/
│   └── DiscordBot/
│       ├── Commands/           # Command implementations
│       ├── Services/           # Bot services and dependency injection
│       ├── Models/             # Data models and configuration
│       ├── appsettings.json    # Configuration file
│       └── Program.cs          # Entry point
├── README.md
└── LICENSE
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🐛 Troubleshooting

### Common Issues

- **Bot not responding**: Check if the bot token is correct and the bot is online
- **Permission errors**: Ensure the bot has necessary permissions in your Discord server
- **Commands not found**: Verify that command classes inherit from `BaseCommand` and have the `[DiscordCommand]` attribute

### Getting Help

If you encounter issues:
1. Check the console output for error messages
2. Verify your `appsettings.json` configuration
3. Ensure your bot has proper Discord permissions
4. Create an issue on GitHub with detailed information about the problem

---

**Made with ❤️ and C#**