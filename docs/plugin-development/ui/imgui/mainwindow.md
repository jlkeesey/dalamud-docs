# Main and Config Windows

Dalamud has a simple windowing system for handling the plugin's windows. It has
direct support for a main window and a configuration window. The `Window` class
provides simplified support for some basic window features like sizing as well
as certain lifetime events.

## Main Window

Dalamud has support for a main window for your plugin which provides a place to
display whatever information your plugin needs. It is not required to have a
main window, but most do.

Once you've created your window (see [Window](./window)) you hook it into the
Dalamud system like this:

```csharp
dalamudPluginInterface.UIBuilder.OpenMainUi += ToggleMain;

// ...

public void ToggleMain()
{
    _mainWindow.Toggle();
}
```

This allows Dalamud to open your main window from the installed plugins page.
Normally you will also create one or more commands to show your window.

### Cleanup

Remember to deregister your window when you plugin is shutdown:

```csharp
dalamudPluginInterface.UIBuilder.OpenMainUi -= ToggleMain;
```

## Config Window

Dalamud has support for a configuration window for your plugin which provides a
place to display whatever configuration your plugin needs. It is not required to
have a config window, but most do.

Once you've created your window (see [Window](./window)) you hook it into the
Dalamud system like this:

```csharp
dalamudPluginInterface.UIBuilder.OpenConfigUi += ToggleConfig;

// ...

public void ToggleConfig()
{
    _configWindow.Toggle();
}
```

This allows Dalamud to open your config window from the installed plugins page.
Normally you will also create one or more commands to show your window.

### Cleanup

Remember to deregister your window when you plugin is shutdown:

```csharp
dalamudPluginInterface.UIBuilder.OpenConfigUi -= ToggleConfig;
```
