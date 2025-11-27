# Finity UI Library - Complete Documentation

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Getting Started](#getting-started)
4. [Window Creation](#window-creation)
5. [Categories](#categories)
6. [Sectors](#sectors)
7. [Cheat Types](#cheat-types)
8. [Notifications](#notifications)
9. [Themes](#themes)
10. [Advanced Features](#advanced-features)
11. [Examples](#examples)

---

## Introduction

Finity is a feature-rich UI library for Roblox executors with a clean, modern design. It supports multiple cheat types, custom themes, notifications, and persistent storage.

**Key Features:**
- Multiple pre-built themes (Dark, Light)
- Custom theme support
- Toast notifications
- Persistent storage across sessions
- Keybind system
- Multi-dropdown support
- Customizable toggle key

---

## Installation

```lua
local finity = loadstring(game:HttpGet("https://raw.githubusercontent.com/myethg/finity-fork/main/Library"))()
```

---

## Getting Started

### Basic Setup

```lua
local finity = loadstring(game:HttpGet("https://raw.githubusercontent.com/myethg/finity-fork/main/Library"))()

local window = finity.new(
    "My GUI",      -- Title
    true,          -- IsDark (true/false)
    false,         -- CustomTheme (true/false)
    nil,           -- CustomThemeName
    false,         -- HideToolTip
    "v1.0.0"       -- ToolTipText
)
```

---

## Window Creation

### `finity.new(Title, IsDark, CustomTheme, CustomThemeName, HideToolTip, ToolTipText)`

Creates a new Finity window.

**Parameters:**
- `Title` (string): The title displayed at the top of the window
- `IsDark` (boolean): Whether to use dark theme (true) or light theme (false)
- `CustomTheme` (boolean): Whether to use a custom theme
- `CustomThemeName` (string): Name of the custom theme (if CustomTheme is true)
- `HideToolTip` (boolean): Whether to hide the tooltip text
- `ToolTipText` (string): Additional text displayed next to the title

**Example:**
```lua
local window = finity.new("MyScript", true, false, nil, false, "Version 1.5")
```

---

## Categories

Categories are the main navigation sections in your GUI.

### `window:Category(name)`

Creates a new category tab.

**Parameters:**
- `name` (string): The name of the category

**Returns:** Category object

**Example:**
```lua
local combat = window:Category("Combat")
local visuals = window:Category("Visuals")
local misc = window:Category("Misc")
```

---

## Sectors

Sectors are subsections within categories that organize cheats.

### `category:Sector(name)`

Creates a new sector within a category.

**Parameters:**
- `name` (string): The name of the sector

**Returns:** Sector object

**Example:**
```lua
local aimbot = combat:Sector("Aimbot")
local esp = visuals:Sector("ESP")
```

---

## Cheat Types

### 1. Checkbox/Toggle

A simple on/off switch.

```lua
sector:Cheat("checkbox", "Cheat Name", function(enabled)
    print("Checkbox is now:", enabled)
end, {
    enabled = false  -- default state (optional)
})
```

**Parameters:**
- `enabled` (boolean): Default enabled state

**Callback:** Returns `true` when enabled, `false` when disabled

---

### 2. Label

Displays text information (no interaction).

```lua
local label = sector:Cheat("label", "Status: Ready")
```

**Methods:**
```lua
label:SetValue("New Text")
```

---

### 3. Button

A clickable button that executes a function.

```lua
sector:Cheat("button", "Button Label", function()
    print("Button clicked!")
end, {
    text = "Click Me"  -- button text
})
```

**Parameters:**
- `text` (string): The text displayed on the button

**Methods:**
```lua
button:Fire()  -- programmatically trigger the button
```

---

### 4. Slider

A draggable slider for numeric values.

```lua
local slider = sector:Cheat("slider", "Speed", function(value)
    print("Slider value:", value)
end, {
    min = 0,           -- minimum value
    max = 100,         -- maximum value
    default = 50,      -- starting value
    suffix = " studs", -- text after the value
    precise = false    -- true for decimals, false for integers
})
```

**Parameters:**
- `min` (number): Minimum value
- `max` (number): Maximum value
- `default` (number): Starting value
- `suffix` (string): Text displayed after the value
- `precise` (boolean): Enable decimal values

**Methods:**
```lua
slider:SetValue(75)
```

---

### 5. Textbox

An input field for text/numbers.

```lua
local textbox = sector:Cheat("textbox", "Username", function(text)
    print("Input:", text)
end, {
    placeholder = "Enter username..."  -- placeholder text
})
```

**Parameters:**
- `placeholder` (string): Placeholder text when empty

**Methods:**
```lua
textbox:SetValue("NewText")
```

---

### 6. Dropdown

A dropdown menu with single selection.

```lua
local dropdown = sector:Cheat("dropdown", "Select Option", function(selected)
    print("Selected:", selected)
end, {
    options = {"Option 1", "Option 2", "Option 3"},
    default = "Option 1"  -- starting selection
})
```

**Parameters:**
- `options` (table): Array of selectable options
- `default` (string): Initially selected option

**Methods:**
```lua
dropdown:SetValue("Option 2")
dropdown:AddOption("New Option")
dropdown:RemoveOption("Option 1")
```

---

### 7. Multi-Dropdown

A dropdown menu with multiple selections.

```lua
local multidrop = sector:Cheat("multidropdown", "Select Multiple", function(selected)
    print("Selected items:", table.concat(selected, ", "))
end, {
    options = {"Item 1", "Item 2", "Item 3"},
    default = {}  -- starting selections (empty or array)
})
```

**Parameters:**
- `options` (table): Array of selectable options
- `default` (table): Initially selected options (array)

**Methods:**
```lua
multidrop:SetValue({"Item 1", "Item 3"})
multidrop:AddOption("New Item")
multidrop:RemoveOption("Item 1")
```

---

### 8. Color Picker

A color selection tool using HSV bars.

```lua
local colorpicker = sector:Cheat("colorpicker", "ESP Color", function(color)
    print("Selected color:", color)
end, {
    color = Color3.fromRGB(255, 0, 0)  -- default color
})
```

**Parameters:**
- `color` (Color3): Default color

**Usage:**
- Left-click and drag: Select hue
- Right-click and drag: Select brightness

**Methods:**
```lua
colorpicker:SetValue(Color3.fromRGB(0, 255, 0))
```

---

### 9. Keybind

A keybind selector that triggers when the key is pressed.

```lua
local keybind = sector:Cheat("keybind", "Toggle Key", function(key)
    if key then
        print("Key pressed:", key.Name)
    else
        print("Keybind cleared")
    end
end, {
    default = Enum.KeyCode.E  -- default key (optional)
})
```

**Parameters:**
- `default` (Enum.KeyCode): Default keybind

**Usage:**
- Left-click: Set new keybind (press any key)
- Right-click: Clear keybind
- Backspace: Clear keybind while setting

**Methods:**
```lua
keybind:SetValue(Enum.KeyCode.F)
```

**Properties:**
```lua
keybind.holding  -- true when key is being held
keybind.value    -- current KeyCode or nil
```

---

## Notifications

### Toast Notifications

Display temporary notifications to the user.

```lua
window:ToastMessage(
    "Title",           -- Top text
    "Message content", -- Bottom text
    5,                 -- Duration in seconds
    "Info",            -- Alert type: "Info", "Warning", "Success"
    nil                -- Custom background icon (optional)
)
```

**Alert Types:**
- `"Info"` - Blue information icon
- `"Warning"` - Orange warning icon
- `"Success"` - Green success checkmark

**Example:**
```lua
window:ToastMessage("Success!", "Script loaded successfully", 3, "Success")
window:ToastMessage("Warning", "Low health detected", 5, "Warning")
window:ToastMessage("Info", "Press HOME to toggle GUI", 4, "Info")
```

**Features:**
- Click notification to dismiss early
- Automatic queue system for multiple notifications
- Smooth animations

---

## Themes

### Built-in Themes

Finity includes two pre-built themes:

1. **Dark Theme** (default)
2. **Light Theme**

```lua
-- Use dark theme
local window = finity.new("MyGUI", true, false, nil, false, "v1.0")

-- Use light theme
local window = finity.new("MyGUI", false, false, nil, false, "v1.0")
```

---

### Custom Themes

#### Creating a Custom Theme

1. Create a custom theme file:

```lua
-- Customthemes.lua
local CustomThemes = {}

CustomThemes.CustomThemes = {
    ["MyTheme"] = {
        main_container = Color3.fromRGB(20, 20, 25),
        separator_color = Color3.fromRGB(50, 50, 55),
        text_color = Color3.fromRGB(255, 255, 255),
        
        category_button_background = Color3.fromRGB(40, 40, 45),
        category_button_border = Color3.fromRGB(60, 60, 65),
        
        checkbox_checked = Color3.fromRGB(100, 200, 100),
        checkbox_checked_inner = Color3.fromRGB(120, 220, 120),
        checkbox_outer = Color3.fromRGB(70, 70, 75),
        checkbox_inner = Color3.fromRGB(100, 100, 105),
        
        slider_color = Color3.fromRGB(100, 200, 100),
        slider_color_sliding = Color3.fromRGB(120, 220, 120),
        slider_background = Color3.fromRGB(70, 70, 75),
        slider_text = Color3.fromRGB(200, 200, 200),
        
        textbox_background = Color3.fromRGB(60, 60, 65),
        textbox_background_hover = Color3.fromRGB(80, 80, 85),
        textbox_text = Color3.fromRGB(200, 200, 200),
        textbox_text_hover = Color3.fromRGB(255, 255, 255),
        textbox_placeholder = Color3.fromRGB(120, 120, 125),
        
        dropdown_background = Color3.fromRGB(60, 60, 65),
        dropdown_text = Color3.fromRGB(200, 200, 200),
        dropdown_text_hover = Color3.fromRGB(255, 255, 255),
        dropdown_scrollbar_color = Color3.fromRGB(100, 100, 105),
        dropdown_scrollbar_thickness = 4,
        
        button_background = Color3.fromRGB(60, 60, 65),
        button_background_hover = Color3.fromRGB(80, 80, 85),
        button_background_down = Color3.fromRGB(50, 50, 55),
        
        scrollbar_color = Color3.fromRGB(100, 100, 105),
        
        notification_warn = Color3.fromRGB(255, 165, 0),
        notification_success = Color3.fromRGB(0, 255, 0),
        notification_info = Color3.fromRGB(200, 200, 200),
        
        NotifSound = "FinityGUI/assets/NotifSound.wav",
    }
}

return CustomThemes
```

2. Load the custom theme:

```lua
finity.ImportCustomThemes()  -- loads from FinityGUI/Customthemes.lua

local window = finity.new(
    "MyGUI",
    true,          -- can be true or false
    true,          -- CustomTheme = true
    "MyTheme",     -- name of your custom theme
    false,
    "v1.0"
)
```

---

### Downloading Custom Assets

You can download custom assets for themes from the internet.

```lua
finity:DownloadCustomAsset(
    "https://example.com/myasset.png",  -- URL
    "myasset.png",                       -- Asset name
    false                                -- IsCustomThemeFile
)

-- To download a custom theme file
finity:DownloadCustomAsset(
    "https://example.com/theme.lua",
    nil,
    true  -- IsCustomThemeFile
)
```

---

## Advanced Features

### Change Toggle Key

Change the key used to show/hide the GUI.

```lua
window:ChangeToggleKey("Insert")  -- changes to Insert key
```

**Default:** `Home` key

---

### Change Window Title

Update the window title dynamically.

```lua
window:setTitle("New Title")
```

---

### Change Background Image

Set a custom background image for the window.

```lua
window:ChangeBackgroundImage(
    "FinityGUI/assets/custom/myimage.png",  -- Image path
    0.5                                      -- Transparency (0-1)
)
```

---

### Enable Thin Project Mode

Makes the GUI narrower (single column layout).

```lua
window:EnableThinProject(true)
```

---

### Enable Hub Mode

Disables startup messages (useful for script hubs).

```lua
finity:EnableHubMode(true)
```

---

### Play Sounds

Play custom sounds through the GUI.

```lua
finity:PlaySound("FinityGUI/assets/NotifSound.wav")
```

---

### Re-download Assets

Re-download all GUI assets if corrupted.

```lua
finity:RedownloadAssets()
```

---

### Enable Debug Mode

Enable debug logging for development.

```lua
finity:EnableDebugging(true)
```

---

## Examples

### Complete Script Example

```lua
local finity = loadstring(game:HttpGet("https://raw.githubusercontent.com/myethg/finity-fork/main/Library"))()

-- Create window
local window = finity.new("MyScript", true, false, nil, false, "v2.0")

-- Create categories
local combat = window:Category("Combat")
local player = window:Category("Player")

-- Create sectors
local aimbot_sector = combat:Sector("Aimbot")
local movement_sector = player:Sector("Movement")

-- Aimbot toggle
local aimbot_enabled = aimbot_sector:Cheat("checkbox", "Enable Aimbot", function(enabled)
    print("Aimbot:", enabled)
end)

-- FOV slider
local fov_slider = aimbot_sector:Cheat("slider", "FOV", function(value)
    print("FOV:", value)
end, {
    min = 50,
    max = 200,
    default = 90,
    suffix = "°",
    precise = false
})

-- Aimbot key
local aimbot_key = aimbot_sector:Cheat("keybind", "Aimbot Key", function(key)
    if key then
        print("Aimbot key set to:", key.Name)
    end
end, {
    default = Enum.KeyCode.E
})

-- Speed slider
local speed = movement_sector:Cheat("slider", "Walk Speed", function(value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end, {
    min = 16,
    max = 200,
    default = 16,
    suffix = " studs",
    precise = true
})

-- Jump power
local jumppower = movement_sector:Cheat("slider", "Jump Power", function(value)
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
end, {
    min = 50,
    max = 300,
    default = 50,
    precise = false
})

-- Infinite jump
local infjump = movement_sector:Cheat("checkbox", "Infinite Jump", function(enabled)
    print("Infinite Jump:", enabled)
end)

-- Show success notification
window:ToastMessage("Success", "Script loaded successfully!", 3, "Success")
```

---

### Auto-Sell with Multi-Dropdown Example

```lua
local finity = loadstring(game:HttpGet("https://raw.githubusercontent.com/myethg/finity-fork/main/Library"))()

local window = finity.new("Auto Sell", true, false, nil, false, "v1.0")
local automation = window:Category("Automation")
local sell_sector = automation:Sector("Auto Sell")

local items_to_sell = {}
local all_items = {"Apple", "Banana", "Orange", "Grape", "Melon"}

-- Auto sell toggle
local autosell = sell_sector:Cheat("checkbox", "Enable Auto Sell", function(enabled)
    print("Auto Sell:", enabled)
end)

-- Declare selector first
local item_selector

-- Select all button
sell_sector:Cheat("button", "Select All", function()
    if item_selector then
        item_selector:SetValue(all_items)
    end
end, {
    text = "Select All"
})

-- Deselect all button
sell_sector:Cheat("button", "Deselect All", function()
    if item_selector then
        item_selector:SetValue({})
    end
end, {
    text = "Clear Selection"
})

-- Multi-dropdown for item selection
item_selector = sell_sector:Cheat("multidropdown", "Items to Sell", function(selected)
    items_to_sell = selected
    print("Will sell:", table.concat(items_to_sell, ", "))
end, {
    options = all_items,
    default = {}
})

-- Auto sell loop
spawn(function()
    while wait(1) do
        if autosell.value and #items_to_sell > 0 then
            for _, item in pairs(items_to_sell) do
                print("Selling:", item)
                -- Your sell logic here
            end
        end
    end
end)
```

---

### Theme Switching Example

```lua
local finity = loadstring(game:HttpGet("https://raw.githubusercontent.com/myethg/finity-fork/main/Library"))()

-- Import custom themes
finity.ImportCustomThemes()

-- Create window with custom theme
local window = finity.new(
    "Theme Demo",
    true,
    true,           -- Use custom theme
    "CyberpunkTheme", -- Your custom theme name
    false,
    "Custom Theme"
)

-- Rest of your GUI code...
```

---

## Tips & Best Practices

1. **Organization:** Use categories and sectors to keep your GUI organized
2. **Callbacks:** Always handle errors in callbacks with `pcall`
3. **Performance:** Don't put heavy computations in slider callbacks
4. **Keybinds:** Check `keybind.holding` for hold-to-activate features
5. **Notifications:** Use appropriate alert types for better UX
6. **Testing:** Enable debug mode during development
7. **Storage:** Use persistent storage for saving user preferences
8. **Multi-Dropdowns:** Perfect for selecting multiple items/features at once

---

## Common Issues

### GUI not showing
- Make sure your executor supports `CoreGui`
- Check if the GUI was destroyed accidentally
- Verify the script loaded without errors

### Assets not loading
- Run `finity:RedownloadAssets()` to re-download
- Check if your executor supports `writefile`

### Keybinds not working
- Make sure the key isn't already in use
- Check if `UserInputService` is accessible
- Verify the keybind callback is set correctly

### Theme not applying
- Ensure theme name matches exactly (case-sensitive)
- Check if `ImportCustomThemes()` was called
- Verify custom theme file exists in FinityGUI folder

---

## Credits

Finity UI Library by the Finity team
Fork maintained by myethg

For support, bug reports, or suggestions, join the Discord server (link in the library code).

---

**Last Updated:** 2024
**Version:** 1.0.2 (4)