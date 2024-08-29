# WindowSystem

Each plugin should create a `WindowSystem` object and register all windows that
are created with this object. Based on the way that ImGui works, each window
must be drawn and all windows registered with the window system will be drawn
when needed. Managing your own drawing is not supported by the Dalamud team.

### Construction

A `WindowSystem` is created with a namespace that serves to isolate all of your
windows for any other plugin's windows.

```csharp
WindowSystem(string namespace)
```

<dl>
    <dt>namespace</dt>
    <dd>The unique namespace for this plugin. Usually this is the name of the
    plugin.</dd>
</dl>

### Adding Windows

```csharp
AddWindow(Window window)
```

<dl>
    <dt>window</dt>
    <dd>The window to add to the system. The name of the window must be unique
    amongst the registered windows.</dd>
</dl>

Adds the window to the window system. The window will be drawn whenever the
window system is required to draw its windows.

### Removing Windows

```csharp
RemoveWindow(Window window)
```

<dl>
    <dt>window</dt>
    <dd>The window to remove from the system. The name of the window must match
    one of the previously added windows.</dd>
</dl>

Removes the window from the window system. The window will no longer be drawn
whenever the window system is required to draw its windows. This will not
dispose of the window if it is `IDisposable`. You will need to dispose of it
yourself.

### Drawing

```csharp
Draw()
```

For the windows in the window system to be drawn when Dalamud goes to draw
windows, Dalamud needs to know how to draw then. This is done by registering the
`WindowSystem.Draw()` method with the global draw chain:

```csharp
dalamudPluginInterface.UIBuilder.Draw += windowSystem.Draw;
```

where `dalamudPluginInterface` is the `IDalamudPluginInterface` passed into the
plugin's constructor.

When you register the draw callback with the `UIBuilder` you **must** remove the
callback when your plugin is disposed:

```csharp
dalamudPluginInterface.UIBuilder.Draw -= windowSystem.Draw;
```

Failure to do so may cause dire consequences including the game exiting.
