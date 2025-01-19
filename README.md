### ValveFlicker Module Documentation

#### Preamble

I created this module to address a common problem I noticed when working with flickering lights. Most developers end up copying and pasting scripts across multiple lights and rely on `wait` or `TweenService`, which is messy and can impact performance significantly. Inspired by the light flickering implementation in Half-Life and Quake (which is still in use by Valve), I designed this module to offer a cleaner, more performant approach. Instead of using individual timers or tweens for each light, it uses a single RunService.Heartbeat connection to manage all flickering lights centrally, significantly reducing overhead. With predefined and customizable patterns, it allows for efficient management of flickering effects without repetitive scripting.

---

### Preview
https://github.com/user-attachments/assets/dc91f7b1-184f-4a88-b535-96a5a0a4c6f0

---

### Features

- **Predefined Flicker Styles**: Collection of pre-defined patterns, most of them from Half-Life.
- **Customizable Patterns**: Create your own flicker styles with full control over sequences and timing.
- **Performance-Oriented**: Centralized management of light updates using `RunService.Heartbeat`.
- **Debug Visualization**: Optional debug UI for real-time monitoring of light states.

---

### Installation

1. Copy the `ValveFlicker` module into your Roblox project.
2. Require the module where you need to use it:
   ```lua
   local ValveFlicker = require(path.to.ValveFlicker)
   ```

---

### API Reference

#### `ValveFlicker.startFlicker(light, styleIndex, debug?, startIndex?)`

Starts the flickering effect on a specified light.

- **`light`** *(Instance)*: The `Light` instance to apply the flicker effect.
- **`styleIndex`** *(number)*: The index of the flicker style to use.
- **`debug`** *(boolean, optional)*: Enables debug UI if `true`.
- **`startIndex`** *(number, optional)*: The starting point in the flicker sequence (defaults to `1`).

#### `ValveFlicker.stopFlicker(light, styleIndex)`

Stops the flickering effect on a specified light.

- **`light`** *(Instance)*: The `Light` instance to stop flickering.
- **`styleIndex`** *(number)*: The index of the flicker style being used.

#### `ValveFlicker.createCustomStyle(styleIndex, sequence, transitionTime?)`

Creates a custom flicker style.

- **`styleIndex`** *(number)*: A unique index for the new style.
- **`sequence`** *(string)*: The flicker pattern (e.g., `"mmamam"`).
- **`transitionTime`** *(number, optional)*: Duration of each step in the sequence (defaults to `0.1` seconds).

#### `ValveFlicker.removeStyle(styleIndex)`

Removes a flicker style, stopping all lights using it.

- **`styleIndex`** *(number)*: The index of the style to remove.

---

### Example Usage

Example 1:
```lua
local ValveFlicker = require(path.to.ValveFlicker)

-- Start flickering with a predefined style (e.g., style 1 - fluorescent flicker)
ValveFlicker.startFlicker(workspace.Light, 1, true)

-- Create a custom style and apply it to a light
ValveFlicker.createCustomStyle(100, "aabbcc", 0.2)
ValveFlicker.startFlicker(workspace.CustomLight, 100)

-- Stop flickering
ValveFlicker.stopFlicker(workspace.Light, 1)
```

Example 2:
```lua
local ValveFlicker = require(game.ReplicatedStorage.ValveFlicker)
local light2 = script.Parent

ValveFlicker.createCustomStyle(500, "azzazzzazzmmazzmazmm")
ValveFlicker.startFlicker(light2, 500, true)
```

```lua
local ValveFlicker = require(game.ReplicatedStorage.ValveFlicker)
local light1 = script.Parent

ValveFlicker.startFlicker(light1, 500, true)
```
---

### Default Flicker Styles

The following styles are available out of the box:

| **Index** | **Pattern**                          | **Description**                  |
|-----------|--------------------------------------|----------------------------------|
| 0         | `"m"`                                | Normal                           |
| 1         | `"mmamammmmammamamaaamammma"`        | Fluorescent flicker              |
| 2         | `"abcdefghijklmnopqrstuvwxyzyxwvutsrqponmlkjihgfedcba"` | Slow strong pulse      |
| 3         | `"mmmmmaaaaammmmmaaaaaabcdefgabcdefg"` | Candle                           |
| 4         | `"mamamamamama"`                     | Fast strobe                      |
| 5         | `"jklqrstuvwxyzyxwvutsrqponmlkj"`    | Gentle pulse                     |
| 6         | `"nmonqnmomnmomomno"`               | Flicker                          |
| 7         | `"mmmaaaabcdefgmmmmaaaammmaamm"`    | Candle 2                         |
| 8         | `"mmmaaammmaaammmabcdefaaaammmmabcdefmmmaaaa"` | Candle 3           |
| 9         | `"aaaaaaaazzzzzzzz"`                | Slow strobe                      |
| 10        | `"mmamammmmammamamaaamammma"`       | Fluorescent flicker 2            |
| 11        | `"abcdefghijklmnopqrrqponmlkjihgfedcba"` | Slow pulse (no fade to black) |

---

### Customizable Patterns

When creating custom flicker styles with `ValveFlicker.createCustomStyle`, the `sequence` parameter uses a simple letter-based brightness mapping:

- The `sequence` is a string of lowercase letters (`a` through `z`).
- Each letter represents a brightness level, with `'a'` being the dimmest and `'z'` being the brightest.
- Intermediate letters represent brightness levels between the minimum and maximum.

For example:

- `"a"`:  Very dim light.
- `"m"`:  Mid-level brightness.
- `"z"`:  Fully bright.
- `"mmamam"`: A pattern that flickers around the mid-level brightness.
- `"aaaaaaaazzzzzzzz"`: A slow strobe effect transitioning from dim to bright.

---

### Debugging

Enable debug visualization by passing `true` to the `debug` parameter in `startFlicker`. This displays a `BillboardGui` with brightness and sequence information above the light.

---

### License

This module is distributed under the MIT License. Feel free to use and modify it in your projects.
