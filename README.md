# Monoprice Zone Card

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://github.com/hacs/integration)

A custom Lovelace card for controlling Monoprice 6-Zone Amplifier zones in Home Assistant.

![Card Preview](images/card-preview.png)

## Features

- Compact, clean design optimized for zone control
- Power toggle with visual state indication
- Volume slider with mute button
- Source selector dropdown
- Optional tone controls (treble, bass, balance)
- Balance slider with center indicator
- Smooth drag interactions (no jitter during adjustment)
- Touch and mouse support

## Installation

### HACS (Recommended)

1. Open HACS in Home Assistant
2. Click the three dots in the top right corner
3. Select "Custom repositories"
4. Add this repository URL with category "Lovelace"
5. Click "Install"
6. Add the resource in your Lovelace configuration

### Manual Installation

1. Download `monoprice-zone-card.js` from the `dist` folder
2. Copy it to your `config/www/` directory
3. Add the resource to your Lovelace configuration:

```yaml
resources:
  - url: /local/monoprice-zone-card.js
    type: module
```

## Configuration

### Basic Configuration

```yaml
type: custom:monoprice-zone-card
media_player: media_player.monoprice_zone_1
```

### Full Configuration

```yaml
type: custom:monoprice-zone-card
name: Living Room
media_player: media_player.monoprice_zone_1
treble: number.monoprice_zone_1_treble
bass: number.monoprice_zone_1_bass
balance: number.monoprice_zone_1_balance
show_tone_controls: true
```

### Configuration Options

| Option | Type | Required | Default | Description |
|--------|------|----------|---------|-------------|
| `media_player` | string | **Yes** | - | Entity ID of the zone's media player |
| `name` | string | No | Entity name | Display name for the zone |
| `treble` | string | No | - | Entity ID for treble control |
| `bass` | string | No | - | Entity ID for bass control |
| `balance` | string | No | - | Entity ID for balance control |
| `show_tone_controls` | boolean | No | `true` | Show/hide treble, bass, balance controls |

## Usage with Monoprice Enhanced Integration

This card is designed to work with the [Monoprice Enhanced](https://github.com/derwoodums/monoprice-enhanced) custom integration, which provides the treble, bass, and balance number entities.

If using the core Monoprice integration, you can still use this card but without tone controls:

```yaml
type: custom:monoprice-zone-card
media_player: media_player.monoprice_zone_1
show_tone_controls: false
```

## Multiple Zones Example

Create a vertical stack for all your zones:

```yaml
type: vertical-stack
cards:
  - type: custom:monoprice-zone-card
    name: Living Room
    media_player: media_player.monoprice_zone_1
    treble: number.monoprice_zone_1_treble
    bass: number.monoprice_zone_1_bass
    balance: number.monoprice_zone_1_balance

  - type: custom:monoprice-zone-card
    name: Kitchen
    media_player: media_player.monoprice_zone_2
    treble: number.monoprice_zone_2_treble
    bass: number.monoprice_zone_2_bass
    balance: number.monoprice_zone_2_balance

  - type: custom:monoprice-zone-card
    name: Master Bedroom
    media_player: media_player.monoprice_zone_3
    treble: number.monoprice_zone_3_treble
    bass: number.monoprice_zone_3_bass
    balance: number.monoprice_zone_3_balance
```

## Control Ranges

| Control | Range | Notes |
|---------|-------|-------|
| Volume | 0-100% | Maps to amplifier's 0-38 range |
| Treble | 0-14 | 7 = flat |
| Bass | 0-14 | 7 = flat |
| Balance | 0-20 | 10 = center, 0 = full left, 20 = full right |

## Visual Indicators

- **Power button**: Blue when on, gray when off
- **Mute button**: Red with X icon when muted, gray speaker icon when unmuted
- **Balance slider**: Center tick mark at 50% indicates balanced audio

## Troubleshooting

### Card not appearing
- Clear browser cache or add `?v=X` to the resource URL
- Verify the resource is added as type `module`

### Sliders not responding
- Ensure entities exist and are available
- Check browser console for errors

### Card shows "Entity not found"
- Verify entity IDs are correct
- Ensure the Monoprice integration is properly configured

## License

MIT License - see [LICENSE](LICENSE) file for details.
