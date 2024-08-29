# Window

Plugin windows all inherit from `Dalamud.Interface.Windowing.Window`.

There are callbacks for the various lifecycle events that can be overridden. The
basic window lifecycle is something like this (this is not exact, but good
enough to give you the idea):

```csharp
OnOpen()
// ...
while (open) {
    PreOpenCheck()
    Update()
    if (!DrawConditions()) continue;
    PreDraw()
    Draw()
    PostDraw()
}
// ...
OnClose()
```

### OnOpen

```csharp
void OnOpen()
```

This is called once, each time the window goes from closed to open. This is a
good place to setup variables needed by the window such as values from the
configuration.

### PreOpenCheck

```csharp
void PreOpenCheck()
```

This is called before the open state of the window is checked and can be used to
make the final decision about whether a window should open. You can set the
`IsOpen` property to change the state.

### Update

```csharp
void Update()
```

Called on every frame if the window is open, even if the window is collapsed but
not if it is closed.

### DrawConditions

```csharp
bool DrawConditions()
```

If this returns `true` the window is drawn, otherwise it is not. Not being drawn
is not the same as closed. `OnClose()` is not called.

### PreDraw

```csharp
void PreDraw()
```

Called before each `Draw()`. Specifically this is called before checking any of
the conditional values that affect the window such as `Collapsed` and `Position`
so they can be adjusted before the window is drawn.

### Draw

```csharp
void Draw()
```

Where most of the work is done. This is where all of the window contents drawing
code for your window goes. This is often the only method that is overridden.

### PostDraw

```csharp
void PostDraw()
```

Called after the window is drawn.

### OnClose

```csharp
void OnClose()
```

This is called once, each time the window goes from open to closed. Can be used
to clean up anything setup in `OnOpen()` that needs cleaning.
