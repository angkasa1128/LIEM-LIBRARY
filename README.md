# 🎨 LIEM UI LIBRARY

> A modern, sleek, and feature-rich UI library for Roblox exploits.

Version  : 1.0.0
License  : MIT
Author   : Liem


## 📋 TABLE OF CONTENTS

- ✨ Features
- 📦 Installation
- 🚀 Quick Start
- 📖 Documentation
- 🎨 Themes
- 💾 Config System
- ⌨️ Keyboard Shortcuts
- 🖼️ Icons
- 📱 Mobile Support
- 📂 Project Structure
- 🐛 Troubleshooting
- 📜 License


## ✨ FEATURES

- 🎨 Multiple Themes
  4 built-in presets (liem, dark, sunset, neon) + full custom color support

- 🎯 Rich Element Set
  Buttons, toggles, sliders, inputs, dropdowns, multi-selects, keybinds,
  color pickers, progress bars, and more

- 💾 Config System
  Save, load, and delete configurations per game

- 🔔 Notification System
  Animated toast notifications with progress bars

- 🔑 Key System
  Built-in key authentication ("Once" or "Everytime" mode)

- 📱 Mobile Support
  Full touch support with on-screen toggle button

- 🖼️ Icon Pack
  400+ Lucide icons built-in, with support for custom rbxassetid:// and
  https:// icons

- 🎵 Sound Effects
  Subtle UI sounds for clicks, hovers, and toggles

- 🪟 Draggable & Resizable
  Smooth window management with minimize support

- ⚡ Lightweight
  Single-file library, no external dependencies


## 📦 INSTALLATION

### Method 1 — Remote Load (Recommended)

    local liem = loadstring(game:HttpGet("https://raw.githubusercontent.com/UsernameKamu/LiemLib/main/liem.lua"))()

### Method 2 — Local File

    local liem = loadstring(readfile("liem.lua"))()

Note: Replace "UsernameKamu" with your actual GitHub username and repo path.


## 🚀 QUICK START

    -- 1. Load the library
    local liem = loadstring(game:HttpGet("https://raw.githubusercontent.com/UsernameKamu/LiemLib/main/liem.lua"))()

    -- 2. Create a window
    local window = liem.new("My Script", {
        GameName = "GameName",
        Theme = liem.presets["liem"],
    })

    -- 3. Create a tab
    local main = window:tab("Main", "home")

    -- 4. Add elements
    main:section("General")

    main:button("Click Me", function()
        window:notify("Success", "Button clicked!")
    end, "check")

    main:toggle("Enable Feature", false, function(state)
        print("Feature:", state)
    end, "feature_flag")

    main:slider("Speed", 0, 100, 50, function(val)
        print("Speed:", val)
    end, "speed_flag")


## 📖 DOCUMENTATION

### 🔧 Window Creation

    local window = liem.new(title, options)

Options:

    - GameName (string)
      Name used for config folder organization

    - Theme (table)
      Theme preset table (e.g. liem.presets["liem"])

    - AutoLoad (string)
      Config name to auto-load on start

    - KeySystem (string)
      "Once" or "Everytime"

    - KeySettings (table)
      Key configuration (see below)

### 🔑 Key Settings

    KeySettings = {
        Key = {"key1", "key2"},          -- Valid keys
        FileName = "mykey",              -- Saved key filename
        Title = "Liem Key System",
        Subtitle = "Enter your key to continue",
        Note = "Get key from discord.gg/xxx",
        Creator = "Liem"
    }

Modes:

    - "Once"
      Key is saved, no re-entry needed

    - "Everytime"
      Key must be entered each execution

### 📑 Tabs

    local tab = window:tab(name, icon)

Parameters:

    - name (string)
      Tab display name

    - icon (string)
      Icon name (e.g. "home", "sword"), rbxassetid://, or https:// URL

Example:

    local main_tab     = window:tab("Main", "home")
    local combat_tab   = window:tab("Combat", "sword")
    local settings_tab = window:tab("Settings", "settings")

### 🧩 Elements

📌 Section

    tab:section("General")

🔘 Button

    tab:button(text, callback, icon)

    tab:button("Click Me", function()
        print("Clicked!")
    end, "check")

🔀 Toggle

    tab:toggle(text, default, callback, flag)

    tab:toggle("Enable Feature", false, function(state)
        print("Feature:", state)
    end, "feature_flag")

🎚️ Slider

    tab:slider(text, min, max, default, callback, flag, step)

    tab:slider("Speed", 0, 100, 50, function(val)
        print("Speed:", val)
    end, "speed_flag", 1)

Note: Click the value label to type a number directly. On mobile,
+/- buttons appear below the track.

⌨️ Input

    tab:input(text, placeholder, callback, flag)

    tab:input("Player Name", "Enter name...", function(text)
        print("Input:", text)
    end, "name_flag")

📋 Dropdown

    tab:dropdown(text, options, default, callback, flag)

    tab:dropdown("Select Option", {"Option1", "Option2", "Option3"}, "Option1", function(selected)
        print("Selected:", selected)
    end, "dropdown_flag")

Note: Includes a search bar for filtering options.

☑️ Multi-Select

    tab:multiselect(text, options, defaults, callback, flag)

    tab:multiselect("Select Multiple", {"A", "B", "C"}, {"A"}, function(selected)
        for _, v in ipairs(selected) do print(v) end
    end, "multi_flag")

🎨 Color Picker

    tab:colorpicker(text, default, callback, flag)

    tab:colorpicker("Accent Color", Color3.fromRGB(255, 100, 150), function(color)
        window:accent(color)
    end, "color_flag")

🔑 Keybind

    tab:keybind(text, default, hold_to_interact, callback, flag)

    tab:keybind("Toggle Key", "F", false, function()
        print("Keybind pressed!")
    end, "keybind_flag")

Note: Set hold_to_interact = true for hold-mode keybinds (callback
receives true on press, false on release).

📊 Progress Bar

    tab:progressbar(text, max_value)

    local bar = tab:progressbar("Loading", 100)
    bar:set(75, true) -- value, animate

🖼️ Image

    tab:image(asset_id, height, scale_type)

    tab:image("rbxassetid://123456789", 120, Enum.ScaleType.Fit)

📝 Paragraph

    tab:paragraph(title, text)

🏷️ Label

    tab:label("Some descriptive text here")

➖ Spacer

    tab:space(16)

### 🛠️ Utility Functions

🔔 Notification

    window:notify(title, message, duration)

    window:notify("Success", "Script loaded!", 5)

🎨 Change Accent Color

    window:accent(Color3.fromRGB(255, 100, 150))

🎭 Apply Theme

    window:apply_theme({ accent = Color3.fromRGB(100, 200, 255) })

⚙️ Auto Settings Tab

    window:create_settings()

Creates a fully functional Settings tab with:

    - Config save/load/delete
    - Theme preset selector
    - Custom color pickers for all theme properties

🗑️ Destroy UI

    window:destroy()


## 🎨 THEMES

Liem ships with 4 built-in presets. Apply one at creation:

    local window = liem.new("My Script", {
        Theme = liem.presets["liem"]
    })

Presets:

    - liem
      Accent: 🌸 Pink (#FF6496)
      Vibe: Default, vibrant

    - dark
      Accent: 💙 Blue (#64B4FF)
      Vibe: Cool, professional

    - sunset
      Accent: 🧡 Orange (#FF8C50)
      Vibe: Warm, energetic

    - neon
      Accent: 💚 Teal (#00FFC8)
      Vibe: Cyberpunk, modern

### 🎨 Custom Themes

    local window = liem.new("My Script", {
        Theme = {
            bg        = Color3.fromRGB(10, 8, 15),
            container = Color3.fromRGB(16, 14, 22),
            element   = Color3.fromRGB(24, 20, 32),
            hover     = Color3.fromRGB(34, 28, 44),
            active    = Color3.fromRGB(40, 34, 54),
            accent    = Color3.fromRGB(255, 100, 150),
            text      = Color3.fromRGB(245, 240, 255),
            subtext   = Color3.fromRGB(180, 170, 200),
            border    = Color3.fromRGB(40, 34, 54),
        }
    })

Note: Or use the built-in color pickers in the Settings tab at runtime.


## 💾 CONFIG SYSTEM

Configs are saved to: LiemConfigs/<GameName>/<ConfigName>.json

    -- Save current flags to a config
    -- (via Settings tab or manually)

    -- Auto-load on start
    local window = liem.new("My Script", {
        GameName = "MyGame",
        AutoLoad = "main"
    })

Note: All elements with a flag parameter are automatically saved and restored.


## ⌨️ KEYBOARD SHORTCUTS

    - Right Ctrl
      Toggle UI (PC)

    - R3 / Right Stick
      Toggle UI (Mobile)


## 🖼️ ICONS

Liem includes 400+ Lucide icons out of the box. Use icon names directly:

    window:tab("Home", "home")
    window:tab("Combat", "sword")
    window:tab("Settings", "settings-2")
    window:tab("Users", "users")

Note: Browse all available icons in liem.icons.

### 🖼️ Custom Icons

    -- Roblox asset
    window:tab("Custom", "rbxassetid://123456789")

    -- Remote image (downloaded & cached automatically)
    window:tab("Remote", "https://example.com/icon.png")


## 📱 MOBILE SUPPORT

Liem automatically detects mobile devices and:

    - Adds a floating toggle button (bottom-right)
    - Shows +/- buttons on sliders for precision
    - Adjusts element heights for touch targets
    - Handles touch drag for window movement


## 📂 PROJECT STRUCTURE

    LiemConfigs/
    ├── GameName1/
    │   ├── config1.json
    │   └── config2.json
    └── GameName2/
        └── default.json

    liem_icons/
    └── cached_remote_icons.png

    liemlib_logo.png


## 🐛 TROUBLESHOOTING

    - UI doesn't appear
      Solution: Check executor supports getcustomasset, writefile, isfile

    - Icons not loading
      Solution: Ensure request/http_request is available for remote icons

    - Configs not saving
      Solution: Verify writefile and makefolder are supported

    - Key system stuck
      Solution: Check KeySettings.Key table contains valid keys


## 📜 LICENSE

MIT License

Copyright (c) 2025 Liem

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


Made with 💖 by Liem
⭐ Star this repo if you find it useful!
