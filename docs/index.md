# Razor Input

Dead simple input handling for Roblox.

## Installation

Install via Wally:

```toml
RazorInput = "vibeonline/razorinput@0.1.0"
```

## Quick Start

```lua
local RazorInput = require(path.to.RazorInput)

-- Bind a simple action to a key
RazorInput:bindAction(function(pressed)
    print("Space pressed:", pressed)
end, "Space")

-- Bind an axis (e.g., Movement)
local moveAxis = RazorInput.createAxis("W", "S", "A", "D")
RazorInput:bindAxis(function(pressed, direction)
    print("Moving direction:", direction)
end, moveAxis)

-- Connect to UserInputService
local UserInputService = game:GetService("UserInputService")
UserInputService.InputBegan:Connect(function(input)
    RazorInput:input(input)
end)
UserInputService.InputEnded:Connect(function(input)
    RazorInput:input(input)
end)
```

## API Reference

### `InputController`

#### `createAxis(up: string, down: string, left: string, right: string): { string }`
Creates an axis definition for 4-way movement.
- **Returns**: A table containing the key names.

#### `bindAxis(action: (pressed: boolean, direction: Vector3) -> (), ...: { string } | string)`
Binds one or more inputs to an axis action.
- If a table (from `createAxis`) is passed, it calculates a `Vector3` direction based on the pressed keys of that axis.
- `action` is called with `(pressed, direction)`.

#### `bindAction(action: (pressed: boolean, position: Vector3?) -> (), ...: string)`
Binds one or more keys to a specific action.
- **action**: A callback function receiving `pressed` (boolean) and the input `position` (Vector3).

#### `input(inp: InputObject)`
The entry point for processing input. This should be called from `UserInputService.InputBegan` and `UserInputService.InputEnded`.
