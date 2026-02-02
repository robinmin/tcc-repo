# Overview of macOS Process Automation Methods

macOS provides multiple approaches to process automation and service management, each suited for different scenarios. From the native launchd system to language-specific process managers like PM2, understanding these tools is essential for running background services, scheduled tasks, and production applications on macOS.

## Native macOS: launchd

launchd is macOS's init system and service manager, equivalent to systemd on Linux. It manages daemons, agents, and scheduled tasks through launchctl command and plist configuration files.

### LaunchAgents vs LaunchDaemons

- **LaunchAgents** - User-level services that run when you log in (`~/Library/LaunchAgents/`)
- **LaunchDaemons** - System-level services that run at boot (`/Library/LaunchDaemons/`)

### Basic Commands

```bash
launchctl list                    # List all services
launchctl load service.plist      # Load a service
launchctl start com.example.app  # Start a service
```

### Creating a Service

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.myapp</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/node</string>
        <string>/Users/user/app.js</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <true/>
</dict>
</plist>
```

## Homebrew Services

Simple service management for packages installed via Homebrew:

```bash
brew services list              # List all services
brew services start postgresql   # Start a service
brew services stop redis         # Stop a service
```

## Node.js: PM2

Production process manager for Node.js:

```bash
npm install pm2 -g
pm2 start app.js
pm2 startup darwin    # Auto-start on boot
pm2 save              # Save process list
```

## Python: Supervisord/Circus

Process control for Python applications:

```bash
pip install circus
circusd circus.ini
circusctl status
```

## Choosing the Right Tool

| Use Case | Tool |
|----------|------|
| Production service | launchd |
| Node.js app | PM2 |
| Python app | Circus |
| Database | brew services |
| Development | Overmind |

The native launchd system provides the most reliable integration with macOS, while language-specific tools like PM2 offer specialized features for their ecosystems.
