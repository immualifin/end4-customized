# End-4 Quickshell Customized

Customized Quickshell configuration based on [end-4/dots-hyprland](https://github.com/end-4/dots-hyprland).

## Changes from Default Configuration

### Bar Layout (BarContent.qml)

| Area | Components |
|------|------------|
| Left-Center | CPU indicator, Media control (positioned separately) |
| Center | Clock/Date, Workspaces |
| Right | Battery, Volume/Mic, Network, Bluetooth, SysTray |

#### Resource Indicators (Resources.qml)
- **Memory (RAM)**: Hidden
- **Swap**: Hidden  
- **CPU**: Always visible (only resource indicator shown)

#### Media Control (Media.qml)
- Only appears when media is playing
- **Hover behavior**: Title and artist are hidden by default, slide out from the icon when hovering
- **Dynamic width**: Expands on hover with smooth animation using `Appearance.animation.elementMove`
- **No empty space**: When not hovering, only the music icon is shown

#### Battery Indicator
- Moved from center group to right indicator group (alongside volume, network, bluetooth icons)
- Scaled to 0.8 for consistent sizing with other icons

#### Layout Symmetry
- Resources/Media group positioned separately from Clock and Workspaces
- Ensures the center section (Clock + Workspaces) remains truly centered
- Time/Date width auto-fits to content instead of fixed width

#### Component Order in Center
- **Before**: CPU → Workspaces → Clock
- **After**: CPU → Clock → Workspaces

### Panel Families (shell.qml)

- **Waffle Panel**: Added `iiOverview` to enabled panels list, so Task View button works correctly in waffle panel family

### Applications (Config.qml)

- **Task Manager**: Uses `plasma-systemmonitor --page-name Processes`

## Behavior Summary

| Condition | Behavior |
|-----------|----------|
| Media playing (not hovered) | CPU + Music icon only |
| Media playing (hovered) | CPU + Music icon + Title/Artist (slides out) |
| No media playing | CPU indicator only |

## Installation

1. Backup your existing Quickshell configuration
2. Clone this repository to `~/.config/quickshell/ii`
3. Reload Quickshell

```bash
# Backup
mv ~/.config/quickshell/ii ~/.config/quickshell/ii.backup

# Clone
git clone https://github.com/immualifin/end4-costumized.git ~/.config/quickshell/ii

# Reload Quickshell (or restart session)
```

## Dependencies

- [Quickshell](https://github.com/quickshell-mirror/quickshell)
- [Hyprland](https://hyprland.org/)
- `plasma-systemmonitor` (for Task Manager)

## Files Modified

| File | Changes |
|------|---------|
| `modules/ii/bar/BarContent.qml` | Layout restructure, battery moved, media visibility |
| `modules/ii/bar/Resources.qml` | Hide RAM/Swap, show CPU only |
| `modules/ii/bar/Media.qml` | Hover-to-reveal with slide animation |
| `shell.qml` | Added iiOverview to waffle panel family |

## Credits

- Original configuration: [end-4/dots-hyprland](https://github.com/end-4/dots-hyprland)
