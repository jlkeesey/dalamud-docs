# PushColor

This changes one of the ImGui colors such that it will be restored on exit.

```csharp
ImRaii.PushColor(ImGuiCol idx, uint color, bool condition = true)
ImRaii.PushColor(ImGuiCol idx, Vector4 color, bool condition = true)
```

<dl>
    <dt>idx</dt>
    <dd>The color to change from the <code>ImGuiCol</code> enum.</dd>
    <dt>color</dt>
    <dd>The new color value. Colors can be specified as <code>uint</code> e.g.
    0xff123456 or <code>Vector4</code>.</dd>
    <dt>condition</dt>
    <dd>An optional condition value. If this value is <code>false</code>, then
    this color change does not take place. This can help with the readability,
    especially with multiple color changes.</dd>
</dl>

### Example

```csharp
using (ImRaii.PushColor(ImGuiCol.Text, 0xff0000ff)) {
    // Do some stuff with text color set to red
}
```

### Replaces

```csharp
if (ImGui.PushColor(ImGuiCol.Text, 0xff0000ff)) {
    // Do some stuff with text color set to red

    ImGui.PopColor();
}
```

But the ImRaii works correctly in case of an exception.

### Multiple Color Changes

It is often the case the you want to change multiple colors at the same time,
e.g. both the button normal, hovered, and active colors. You can do it this way:

```csharp
using (ImRaii.PushColor(ImGuiCol.Button, 0xbb0000ff)) {
using (ImRaii.PushColor(ImGuiCol.ButtonHovered, 0xee0000ff)) {
using (ImRaii.PushColor(ImGuiCol.ButtonActive, 0xff0000ff)) {
    // Do some stuff with button colors
}
```

However this will create three different `IDisposable` objects, each of which
will be disposed one right after the other. To handle this case more
efficiently, the object returned can handle chained calls so you can do this:

```csharp
using (ImRaii.PushColor(ImGuiCol.Button, 0xbb0000ff)
             .Push(ImGuiCol.ButtonHovered, 0xee0000ff)
             .Push(ImGuiCol.ButtonActive, 0xff0000ff)) {
    // Do some stuff with button colors
}
```

or if you prefer:

```csharp
using var color = ImRaii.PushColor(ImGuiCol.Button, 0xbb0000ff);
color.Push(ImGuiCol.ButtonHovered, 0xee0000ff);
color.Push(ImGuiCol.ButtonActive, 0xff0000ff);
// Do some stuff with button colors
```

### Popping Colors

It may be useful to pop some or all of the changed colors before the end of the
current block. To do this you can use the `Pop()` method on the `IDisposable`
object:

```csharp
using var color = ImRaii.PushColor(ImGuiCol.Button, 0xbb0000ff);
color.Push(ImGuiCol.ButtonHovered, 0xee0000ff);
color.Push(ImGuiCol.ButtonActive, 0xff0000ff);
// Do some stuff with button colors
color.Pop(2);  // Undo the ButtonActive and ButtonHovered changes
```

At the end of the block, only the remaining, unpopped, values will be restored.
