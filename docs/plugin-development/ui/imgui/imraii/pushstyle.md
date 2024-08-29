# PushStyle

This changes one of the ImGui styles such that it will be restored on exit.

```csharp
ImRaii.PushStyle(ImGuiStyleVar idx, float value, bool condition = true)
ImRaii.PushStyle(ImGuiStyleVar idx, Vector2 value, bool condition = true)
```

<dl>
    <dt>idx</dt>
    <dd>The style to change from the <code>ImGuiStyleVar</code> enum.</dd>
    <dt>value</dt>
    <dd>The new value for the style. Styles take either a <code>float</code> or
    a <code>Vector2</code> value. If the wrong type is passed, an
    <code>ArgumentException</code> is thrown.</dd>
    <dt>condition</dt>
    <dd>An optional condition value. If this value is <code>false</code>, then
    this style change does not take place. This can help with the readability,
    especially with multiple style changes.</dd>
</dl>

### Example

```csharp
using (ImRaii.PushStyle(ImGuiStyleVar.ChildRounding, 5.0f)) {
    // Do some stuff with child rounding set to 5
}
```

### Replaces

```csharp
ImGui.PushStyleVar(ImGuiStyleVar.ChildRounding, 5.0f);
// Do some stuff
ImGui.PopStyleVar();
```

### Multiple Style Changes

It is often the case the you want to change multiple styles at the same time,
e.g. both the window padding and window border size. You can do it this way:

```csharp
using (ImRaii.PushStyle(ImGuiStyleVar.WindowPadding, 10.0f)) {
using (ImRaii.PushStyle(ImGuiStyleVar.WindowBorderSize, 2.0f)) {
using (ImRaii.PushStyle(ImGuiStyleVar.WindowRounding, 5.0f)) {
    // Do some stuff with windows
}
```

However this will create three different `IDisposable` objects, each of which
will be disposed one right after the other. To handle this case more
efficiently, the object returned can handle chained calls so you can do this:

```csharp
using (ImRaii.PushStyle(ImGuiStyleVar.WindowPadding, 10.0f)
             .Push(ImGuiStyleVar.WindowBorderSize, 2.0f)
             .Push(ImGuiStyleVar.WindowRounding, 5.0f)) {
    // Do some stuff with windows
}
```

or if you prefer:

```csharp
using var style = ImRaii.PushStyle(ImGuiStyleVar.WindowPadding, 10.0f);
style.Push(ImGuiStyleVar.WindowBorderSize, 2.0f);
style.Push(ImGuiStyleVar.WindowRounding, 5.0f);
// Do some stuff with windows
```

### Popping Styles

It may be useful to pop some or all of the changed styles before the end of the
current block. To do this you can use the `Pop()` method on the `IDisposable`
object:

```csharp
using var color = ImRaii.PushStyle(ImGuiStyleVar.WindowPadding, 10.0f);
style.Push(ImGuiStyleVar.WindowBorderSize, 2.0f);
style.Push(ImGuiStyleVar.WindowRounding, 5.0f);
// Do some stuff with windows
color.Pop(2);  // Undo the rounding and border size changes
```

At the end of the block, only the remaining, unpopped, values will be restored.
