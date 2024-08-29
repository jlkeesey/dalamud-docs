# PushFont

This changes one of the ImGui colors such that it will be restored on exit.

```csharp
ImRaii.PushFont(ImFontPtr font, bool condition = true)
```

<dl>
    <dt>font</dt>
    <dd>The already loaded font to change to.</dd>
    <dt>condition</dt>
    <dd>An optional condition value. If this value is <code>false</code>, then
    this font change does not take place. This can help with the readability.</dd>
</dl>

### Example

```csharp
using (ImRaii.PushFont(UiBuilder.IconFont)) {
    // Do some stuff with font set to the icon font.
}
```

### Replaces

```csharp
if (ImGui.PushFont(UiBuilder.IconFont)) {
    // Do some stuff with font set to the icon font.

    ImGui.PopFont();
}
```

But the ImRaii works correctly in case of an exception.
