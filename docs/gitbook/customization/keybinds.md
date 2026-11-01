# Opening Shortcuts

BeastMiniMap opens its atlas through logical Minecraft actions, without a client-side keybind mod. A player can choose up to two modifiers and one trigger, subject to the server's permission and shortcut policy.

## Server Defaults

In `config.yml`:

```yaml
Map:
  Enabled: true
  OpenKeybind:
    Enabled: true
    Modifiers:
      - SNEAK
      - SPRINT
    Trigger: SWAP_HAND
    CancelVanillaAction: true
    RequireStandingStill: false
    CooldownMs: 500
```

With unmodified Minecraft controls, this is Shift + Ctrl + F. Players who remap Minecraft's controls use their own physical keys for those same actions.

`Map.Enabled` controls interactive atlas opening. `OpenKeybind.Enabled` controls only shortcut activation; disabling the shortcut does not disable commands. Cooldown, vanilla-action cancellation and the standing-still requirement are server policies that players cannot override.

## Supported IDs

| Type | IDs |
| --- | --- |
| Modifiers | `SNEAK`, `SPRINT` |
| Triggers | `SWAP_HAND`, `DROP_ITEM`, `RIGHT_CLICK`, `LEFT_CLICK` |
| Hotbar triggers | `HOTBAR_1` through `HOTBAR_9` |

Use `Modifiers: []` for no modifier. Matching is exact: a SNEAK-only shortcut does not match if the client reports both SNEAK and SPRINT. Hold the modifiers before activating the trigger.

## Player Choices

The Shortcut page in `/beastminimap map settings` has separate dropdowns for modifiers and trigger. Apply saves the choice; Cancel discards it. The two fields have separate permissions:

> **Screenshot placement:** show the two shortcut selectors and the selected gesture in `12-keybind-settings.png`.

```text
beastminimap.settings.keybind.modifiers
beastminimap.settings.keybind.trigger
```

Players can also use:

```text
/beastminimap keybind
/beastminimap keybind set SNEAK+SWAP_HAND
/beastminimap keybind set SNEAK SPRINT HOTBAR_9
/beastminimap keybind set RIGHT_CLICK
/beastminimap keybind reset
```

`reset` resumes inheritance from the current server default. A saved explicit choice remains unchanged when an administrator changes that default. Changing inheritance for an otherwise identical gesture requires both shortcut-setting grants.

Opening still requires `beastminimap.buttons.open` and normal map eligibility. Changing the keybind does not bypass disabled maps or [gliding restrictions](../maps/atlas.md).

## Vanilla Input Limits

- A hotbar trigger needs an actual slot change. Pressing the already selected slot produces no event. Scrolling to a slot produces the same action as selecting it by number.
- `DROP_ITEM` needs a real item-drop attempt; Q with no item to drop may produce no event.
- Modifier state depends on what the vanilla client reports. Standing SNEAK + SPRINT can be reported, but remapped controls, keyboard rollover and other plugins can affect delivery.
- `CancelVanillaAction: true` cancels supported matching swaps, drops, slot changes and clicks. Client prediction can briefly display an action before cancellation arrives.
- Cooldown values are whole milliseconds from 0 to 60000. Duplicate activations within the same tick are suppressed even at zero.

If a combination is unreliable for a player's controls, use `SNEAK+SWAP_HAND` as a simpler alternative or open the map with a command.
