# fluent_renewed_docs
Documentation for the [Renewed version of Fluent](https://github.com/ActualMasterOogway/Fluent-Renewed) by [ActualMasterOogway](https://github.com/ActualMasterOogway)


# Getting Started

  

## HTTP Installation

  

```lua

local Library = loadstring(game:HttpGetAsync("https://github.com/ActualMasterOogway/Fluent-Renewed/releases/latest/download/Fluent.luau"))()

local SaveManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ActualMasterOogway/Fluent-Renewed/master/Addons/SaveManager.luau"))()

local InterfaceManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ActualMasterOogway/Fluent-Renewed/master/Addons/InterfaceManager.luau"))()

```

  

## Creating a Window

The ```Library:CreateWindow(config)``` function creates the main UI window, which serves as the container for tabs and elements.

```lua

  

local Window = Library:CreateWindow{

Title = "Fluent 1.0.5",

SubTitle = "by Actual Master Oogway",

TabWidth = 160,

Size = UDim2.fromOffset(830, 525),

Resize = true, -- Scales size to 1920x1080 reference

MinSize = Vector2.new(470, 380),

Acrylic = true, -- Enables acrylic blur

Theme = "Dark",

MinimizeKey = Enum.KeyCode.RightControl

}

```

  

### Config Parameters:

```Title``` (string): Window title (supports string formatting, e.g., ```Fluent {Library.Version}```).

  

```SubTitle``` (string, optional): Subtitle below the title.

  

```TabWidth``` (number): Width of the tab sidebar (default: 160).

  

```Size``` (UDim2): Initial window size.

  

```Resize``` (boolean): Scales size based on 1920x1080 resolution (useful for mobile).

  

```MinSize)``` (Vector2): Minimum window size for resizing.

  

```Acrylic``` (boolean): Enables/disables acrylic blur (default: false; may be detectable).

  

```Theme``` (string): Theme name (e.g., "Dark", "Vynixu"). See Themes (#themes).

  

```MinimizeKey``` (Enum.KeyCode): Key to toggle minimization (default: RightControl).

  

Returns: A ```Window``` object for adding tabs and managing the UI.

## Creating Tabs

Tabs organize content within the window. Use Window:CreateTab(config) to add a tab.

```lua

  

local Tabs = {

Main = Window:CreateTab{

Title = "Main",

Icon = "phosphor-users-bold"

},

Settings = Window:CreateTab{

Title = "Settings",

Icon = "settings"

}

}

```

  

### Config Parameters:

```Title``` (string): Tab name.

  

```Icon``` (string, optional): Icon name (e.g., "phosphor-users-bold", "settings") from Lucide or Phosphor libraries.

  

**Returns**: A ```Tab``` object for adding elements.

## Accessing Options

The Library.Options table stores references to interactive elements (e.g., toggles, sliders) by their key (e.g., MyToggle). Use it to get or set values programmatically.

```lua

  

local Options = Library.Options

print(Options.MyToggle.Value) -- Access toggle value

```

## UI Elements

Elements are added directly to tabs (no explicit sections required in this version). Below are the supported elements and their usage.

Paragraph

Displays a title and text content with customizable alignment.

```lua

  

local Paragraph = Tabs.Main:CreateParagraph("Paragraph", {

Title = "Paragraph",

Content = "This is a paragraph.\nSecond line!",

TitleAlignment = "Middle",

ContentAlignment = Enum.TextXAlignment.Center

})

  

print(Paragraph.Value) -- Prints content

Paragraph:SetValue("Updated text!") -- Updates content

```

#### Parameters:

Title (string): Paragraph title.

  

Content (string): Paragraph text (supports newlines).

  

TitleAlignment (string, optional): "Left", "Middle", "Right".

  

ContentAlignment (Enum.TextXAlignment, optional): Text alignment (Left, Center, Right).

  

Methods:

  

```SetValue```(text): Updates the paragraph content.

  

```Value```: Gets the current content.

  

## Button

Creates a clickable button with an optional description.

```lua

  

Tabs.Main:CreateButton{

Title = "Button",

Description = "Very important button",

Callback = function()

Window:Dialog{

Title = "Title",

Content = "This is a dialog",

Buttons = {

{ Title = "Confirm", Callback = function() print("Confirmed") end },

{ Title = "Cancel", Callback = function() print("Cancelled") end }

}

}

end

}

```

  

#### Parameters:

Title (string): Button text.

  

Description (string, optional): Additional text below the title.

  

Callback (function): Function called when clicked.

  

## Toggle

Creates a toggle switch with on/off states.

  

```lua

  

local Toggle = Tabs.Main:CreateToggle("MyToggle", {

Title = "Toggle",

Default = false

})

  

Toggle:OnChanged(function()

print("Toggle changed:", Options.MyToggle.Value)

end)

  

Options.MyToggle:SetValue(true)

```

  

#### Parameters:

  

```Title``` (string): Toggle label.

  

```Default``` (boolean): Initial state.

  

Methods:

  

```OnChanged```(callback): Fires when the toggle changes.

  

```SetValue```(value): Sets the toggle state (accessible via Options[key]).

  

## Slider

Creates a numeric slider with a range.

```lua

  

local Slider = Tabs.Main:CreateSlider("Slider", {

Title = "Slider",

Description = "This is a slider",

Default = 2,

Min = 0,

Max = 5,

Rounding = 1,

Callback = function(Value)

print("Slider changed:", Value)

end

})

  

Slider:OnChanged(function(Value)

print("Slider updated:", Value)

end)

  

Slider:SetValue(3)

```

  

#### Parameters:

Title (string): Slider label.

  

Description (string, optional): Additional text.

  

Default (number): Initial value.

  

Min (number): Minimum value.

  

Max (number): Maximum value.

  

Rounding (number): Decimal places for rounding.

  

Callback (function): Called with new value.

  

Methods:

  

OnChanged(callback): Fires when the value changes.

  

SetValue(value): Sets the slider value.

  

## Dropdown

Creates a dropdown menu (single or multi-select).

```lua

  

local Dropdown = Tabs.Main:CreateDropdown("Dropdown", {

Title = "Dropdown",

Values = {"one", "two", "three"},

Multi = false,

Default = "one"

})

  

Dropdown:OnChanged(function(Value)

print("Dropdown changed:", Value)

end)

  

Dropdown:SetValue("two")

```

  

#### Parameters:

Title (string): Dropdown label.

  

Values (table): List of options.

  

Multi (boolean): Allow multiple selections (default: false).

  

Default (string or table): Initial selection(s).

  

Methods:

  

OnChanged(callback): Fires when selection changes.

  

SetValue(value): Sets the selected value(s) (string for single, table for multi).

  

SetValues(values): Updates the list of options.

  

### Multi-Select Example:

```lua

  

local MultiDropdown = Tabs.Main:CreateDropdown("MultiDropdown", {

Title = "Dropdown",

Description = "You can select multiple values.",

Values = {"one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen"},

Multi = true,

Default = {"seven", "twelve"}

})

  

MultiDropdown:SetValue{

three = true,

five = true,

seven = false

}

  

MultiDropdown:SetValues{"fifteen", "sixteen", "seventeen"}

  

MultiDropdown:OnChanged(function(Value)

local Values = {}

for Value, State in next, Value do

Values[#Values + 1] = Value

end

print("Multidropdown changed:", table.concat(Values, ", "))

end)

```

#### Instance Dropdown Example:

```lua

  

local MultiInstanceDropdown = Tabs.Main:CreateDropdown("MultiInstanceDropdown", {

Title = "Instance Dropdown",

Description = "You can select multiple values and any instance or any other value!",

Values = {workspace, 5, Enum.JoinSource, Enum.MarketplaceBulkPurchasePromptStatus.Error},

Multi = true,

Default = {workspace}

})

  

MultiInstanceDropdown:OnChanged(function(Value)

local Values = {}

for Value, State in next, Value do

Values[#Values + 1] = typeof(Value)

end

print("Multidropdown with instance selection changed:", table.concat(Values, ", "))

end)

```

  

## Colorpicker

Creates a color picker with optional transparency.

```lua

  

local Colorpicker = Tabs.Main:CreateColorpicker("Colorpicker", {

Title = "Colorpicker",

Default = Color3.fromRGB(96, 205, 255)

})

  

Colorpicker:OnChanged(function()

print("Colorpicker changed:", Colorpicker.Value)

end)

  

Colorpicker:SetValueRGB(Color3.fromRGB(0, 255, 140))

```

  

#### Parameters:

Title (string): Colorpicker label.

  

Default (Color3): Initial color.

  

Transparency (number, optional): Initial transparency (0 to 1).

  

Methods:

  

OnChanged(callback): Fires when color or transparency changes.

  

SetValueRGB(color): Sets the color.

  

Transparency Example:

```lua

  

local TColorpicker = Tabs.Main:CreateColorpicker("TransparencyColorpicker", {

Title = "Colorpicker",

Description = "but you can change the transparency.",

Transparency = 0,

Default = Color3.fromRGB(96, 205, 255)

})

  

TColorpicker:OnChanged(function()

print("TColorpicker changed:", TColorpicker.Value, "Transparency:", TColorpicker.Transparency)

end)

```

## Keybind

Creates a keybind input with toggle, hold, or always modes.

```lua

  

local Keybind = Tabs.Main:CreateKeybind("Keybind", {

Title = "KeyBind",

Mode = "Toggle", -- Always, Toggle, Hold

Default = "LeftControl",

Callback = function(Value)

print("Keybind clicked!", Value)

end,

ChangedCallback = function(New)

print("Keybind changed!", New)

end

})

  

Keybind:OnClick(function()

print("Keybind clicked:", Keybind:GetState())

end)

  

Keybind:OnChanged(function()

print("Keybind changed:", Keybind.Value)

end)

  

task.spawn(function()

while  true  do

wait(1)

local state = Keybind:GetState()

if state then

print("Keybind is being held down")

end

if Library.Unloaded then  break  end

end

end)

  

Keybind:SetValue("MB2", "Toggle")

```

  

##### Parameters:

Title (string): Keybind label.

  

Mode (string): "Always", "Toggle", or "Hold".

  

Default (string): Initial key (e.g., "LeftControl", "MB1", "MB2").

  

Callback (function): Called when keybind is activated (true/false).

  

ChangedCallback (function): Called when the keybind is reassigned.

  

Methods:

  

OnClick(callback): Fires when the keybind is toggled (Toggle mode only).

  

OnChanged(callback): Fires when the keybind changes.

  

GetState(): Returns whether the keybind is active.

  

SetValue(key, mode): Sets the key and mode.

  

## Input

  

- Creates a text input field.

```lua

  

local Input = Tabs.Main:CreateInput("Input", {

Title = "Input",

Default = "Default",

Placeholder = "Placeholder",

Numeric = false,

Finished = false,

Callback = function(Value)

print("Input changed:", Value)

end

})

  

Input:OnChanged(function()

print("Input updated:", Input.Value)

end)

```

  

#### Parameters:

Title (string): Input label.

  

Default (string): Initial text.

  

Placeholder (string): Placeholder text.

  

Numeric (boolean): Restrict to numbers (default: false).

  

Finished (boolean): Call callback only on Enter (default: false).

  

Callback (function): Called with new text.

  

### Methods:

  

OnChanged(callback): Fires when the input changes.

  

Dialog

Creates a modal dialog with buttons (triggered via Window:Dialog).

```lua

  

Window:Dialog{

Title = "Title",

Content = "This is a dialog",

Buttons = {

{ Title = "Confirm", Callback = function() print("Confirmed") end },

{ Title = "Cancel", Callback = function() print("Cancelled") end }

}

}

```

#### Parameters:

Title (string): Dialog title.

  

Content (string): Dialog message.

  

Buttons (table): List of buttons with Title and Callback.

  

## Notifications

  

Display notifications using Library:Notify(config).

```lua

  

Library:Notify{

Title = "Notification",

Content = "This is a notification",

SubContent = "Optional details",

Duration = 5  -- Seconds, nil for persistent

}

```

#### Parameters:

Title (string): Notification title.

  

Content (string): Main message.

  

SubContent (string, optional): Secondary message.

  

Duration (number, optional): Time before auto-close.

  

## Addons

  

### SaveManager

The SaveManager addon enables saving and loading user configurations.

```lua

  

SaveManager:SetLibrary(Library)

SaveManager:SetFolder("FluentScriptHub/specific-game")

SaveManager:IgnoreThemeSettings()

SaveManager:SetIgnoreIndexes{}

SaveManager:BuildConfigSection(Tabs.Settings)

SaveManager:LoadAutoloadConfig()

```

Methods:

  

SetLibrary(library): Links to Fluent library.

  

SetFolder(path): Sets config save location.

  

IgnoreThemeSettings(): Excludes theme settings from configs.

  

SetIgnoreIndexes(indexes): Ignores specific elements.

  

BuildConfigSection(tab): Adds save/load UI to a tab.

  

LoadAutoloadConfig(): Loads a marked auto-load config.

  

### InterfaceManager

The InterfaceManager addon manages themes and interface settings.

```lua

  

InterfaceManager:SetLibrary(Library)

InterfaceManager:SetFolder("FluentScriptHub")

InterfaceManager:BuildInterfaceSection(Tabs.Settings)

```

Methods:

  

SetLibrary(library): Links to Fluent library.

  

SetFolder(path): Sets interface save location.

  

BuildInterfaceSection(tab): Adds theme/interface UI to a tab.

  

## Themes

Fluent Renewed supports over 50 themes, including:

- Dark

  

- Light

  

- Vynixu

  

- Amethyst

  

- GitHub Dark

  

- Monokai

  

- Solarized Light

  

Set a theme in the window config or via InterfaceManager UI. Check the GitHub repository for the full list.

Advanced Usage

Selecting a Tab

Select a tab programmatically using Window:SelectTab(index).

```lua

  

Window:SelectTab(1) -- Selects the first tab (Main)

```

## Dynamic Dropdowns

Create large or dynamic dropdowns:

```lua

  

Tabs.Main:CreateButton{

Title = "Really Really big Dropdown",

Description = "",

Callback = function()

local Values = {}

for i = 1, 1000  do

Values[i] = i

end

Tabs.Main:AddDropdown("BIGDropdown", {

Title = "Big Dropdown",

Values = Values,

Multi = false,

Default = 1

})

end

}

```

## Keybind State Checking

Monitor keybind states in a loop:

```lua

  

task.spawn(function()

while  true  do

wait(1)

if Keybind:GetState() then

print("Keybind is being held down")

end

if Library.Unloaded then  break  end

end

end)

```

  

## Instance Dropdowns

Support non-string values in dropdowns:

```lua

  

local MultiInstanceDropdown = Tabs.Main:CreateDropdown("MultiInstanceDropdown", {

Title = "Instance Dropdown",

Description = "You can select multiple values and any instance or any other value!",

Values = {workspace, 5, Enum.JoinSource, Enum.MarketplaceBulkPurchasePromptStatus.Error},

Multi = true,

Default = {workspace}

})

  

MultiInstanceDropdown:OnChanged(function(Value)

local Values = {}

for Value, State in next, Value do

Values[#Values + 1] = typeof(Value)

end

print("Multidropdown with instance selection changed:", table.concat(Values, ", "))

end)

```





