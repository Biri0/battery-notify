# Battery Notify

A simple shell script to notify you when your battery is too low or too high.

## How It Works

This script monitors your battery percentage and charging status. It sends a
desktop notification when:

- The battery drops below a minimum threshold while discharging (default: 40%).
- The battery exceeds a maximum threshold while charging (default: 80%).

To avoid notification spam, the script uses smart threshold-based notifications:

- Notifications are sent at 5% intervals (e.g., 40%, 35%, 30%, 25%...)
- Each threshold only triggers once until the battery status changes
  (charging/discharging)
- When you plug in or unplug the charger, the notification state resets

Notifications are sent using `notify-send`.

## Usage

1. **Make the script executable:**

   ```sh
   chmod +x start.sh
   ```

2. **Run the script:**

   ```sh
   ./start.sh
   ```

   The script will run in a loop, checking your battery status every 5 seconds.

## Hyprland Integration

If you use [Hyprland](https://github.com/hyprwm/Hyprland), you can have the
script start automatically by adding this line to your Hyprland config file
(usually `~/.config/hypr/hyprland.conf`):

```
exec-once = /absolute/path/to/start.sh
```

Replace `/absolute/path/to/start.sh` with the full path to the script.

> **Note:** This script has only been tested on Hyprland.

## Notification Support

This script is known to work with [mako](https://github.com/emersion/mako), the
Wayland notification daemon. Compatibility with other notification daemons is
not guaranteed.

### Fullscreen Notifications with mako

To ensure notifications appear even in fullscreen mode, add the following line
to your `~/.config/mako/config`:

```
layer=overlay
```

This will allow notifications to be displayed above fullscreen windows.

## Configuration

You can adjust the following variables at the top of `start.sh` to suit your
needs:

- `min_bat`: Minimum battery percentage before a low battery notification is
  shown.
- `max_bat`: Maximum battery percentage before a high battery notification is
  shown.
- `seconds`: Interval (in seconds) between checks.

## Requirements

- `notify-send` (usually provided by `libnotify`)
- Access to `/sys/class/power_supply/BAT1/` (may need to adjust if your battery
  device is named differently)
- A compatible notification daemon (tested with mako)

## Disclaimer

This script is provided as-is. Use at your own risk. It has only been tested on
Hyprland with mako.

## License

This project is licensed under the [MIT License](LICENSE).

