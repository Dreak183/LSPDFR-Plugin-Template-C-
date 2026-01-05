# LSPDFR Plugin Template

A Visual Studio project template for creating [LSPDFR](https://www.lcpdfr.com/lspdfr/) (LSPD First Response) plugins for Grand Theft Auto V.

## Features

- Pre-configured project structure for LSPDFR plugin development
- Automatic NuGet package installation (RagePluginHook, RAGENativeUI)
- INI-based settings system with auto-extraction
- Console command registration example
- x64 Release build configuration (optimized for GTA V)
- Configurable GTA V installation path

## Requirements

- Visual Studio 2022 or later
- .NET Framework 4.8
- [Grand Theft Auto V](https://www.rockstargames.com/gta-v)
- [RagePluginHook](https://ragepluginhook.net/)
- [LSPDFR](https://www.lcpdfr.com/lspdfr/)

## Installation

### Option 1: Download Release

1. Download the latest `LSPDFR Plugin Template.zip` from [Releases](../../releases)
2. Copy the zip file to your Visual Studio templates folder:
   ```
   %USERPROFILE%\Documents\Visual Studio 2022\Templates\ProjectTemplates\
   ```
3. Restart Visual Studio

### Option 2: Build from Source

1. Clone this repository
2. Run `CreateTemplate.ps1` to generate the template zip
3. Copy the generated zip to your Visual Studio templates folder

## Usage

### Creating a New Project

1. Open Visual Studio
2. Select **Create a new project**
3. Search for "LSPDFR" or find **LSPDFR Plugin Template**
4. Enter your project name and location
5. Click **Create**

### Configuring GTA V Path

The template references `LSPD First Response.dll` from your GTA V installation. To configure the path:

1. Rename `Directory.Build.props.template` to `Directory.Build.props`
2. Edit the `<GtaVPath>` value to your GTA V installation path:

```xml
<Project>
  <PropertyGroup>
    <GtaVPath>D:\Games\Grand Theft Auto V</GtaVPath>
  </PropertyGroup>
</Project>
```

> **Tip:** Add `Directory.Build.props` to your `.gitignore` so each team member can have their own path configured.

### Building

Build the project using Visual Studio or MSBuild:

```bash
msbuild YourPlugin.csproj /p:Configuration=Release /p:Platform=x64
```

Output will be in `bin\x64\Release\`.

### Deploying

Copy the built DLL to your GTA V plugins folder:

```
Grand Theft Auto V\plugins\LSPDFR\
```

## Project Structure

```
YourPlugin/
├── Properties/
│   └── AssemblyInfo.cs          # Assembly metadata
├── ConsoleCommands.cs           # In-game console commands
├── EntryPoint.cs                # Plugin entry point
├── Settings.cs                  # INI configuration system
├── TemplateSettings.ini         # Default settings (embedded resource)
├── Directory.Build.props        # Local GTA V path configuration
└── YourPlugin.csproj            # Project file
```

### Key Files

| File | Description |
|------|-------------|
| `EntryPoint.cs` | Main plugin class extending `Plugin`. Implements `Initialize()` and `Finally()` lifecycle methods. |
| `ConsoleCommands.cs` | Example console commands using `[ConsoleCommand]` attribute. |
| `Settings.cs` | INI-based configuration with auto-extraction from embedded resource. |
| `TemplateSettings.ini` | Default settings file, embedded and extracted on first run. |

## Dependencies

| Package | Version | Description |
|---------|---------|-------------|
| [RagePluginHook](https://ragepluginhook.net/) | 1.109.1 | Core modding framework for GTA V |
| [RAGENativeUI](https://github.com/alexguirre/RAGENativeUI) | 1.9.3 | UI framework for menus and notifications |
| LSPD First Response | - | Referenced from GTA V installation |

## Example Code

### Console Command

```csharp
[ConsoleCommand("Prints a greeting message")]
public static void HelloWorld()
{
    Game.Console.Print("Hello from my LSPDFR plugin!");
}
```

### Reading Settings

```csharp
// In Settings.cs
public static bool MyFeatureEnabled => SettingsFile.ReadBoolean("General", "MyFeatureEnabled", true);

// Usage
if (Settings.MyFeatureEnabled)
{
    // Feature code
}
```

### Duty State Handler

```csharp
private static void OnOnDutyStateChanged(bool onDuty)
{
    if (onDuty)
    {
        Game.DisplayNotification("Plugin activated!");
    }
}
```

## Troubleshooting

### "LSPD First Response" assembly not found

Ensure your GTA V path is correctly configured in `Directory.Build.props`. The path should point to the root GTA V folder containing the `plugins` subfolder.

### NuGet packages not restoring

Run `nuget restore` or right-click the solution in Visual Studio and select **Restore NuGet Packages**.

## License

This template is provided as-is for the LSPDFR modding community.

## Links

- [LSPDFR Official Website](https://www.lcpdfr.com/lspdfr/)
- [RagePluginHook](https://ragepluginhook.net/)
- [RAGENativeUI GitHub](https://github.com/alexguirre/RAGENativeUI)
- [LSPDFR Plugin Development Guide](https://docs.ragepluginhook.net/)
