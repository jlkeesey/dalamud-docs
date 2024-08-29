# Tooltip

This starts a tooltip component and then ends it when the block ends.

```csharp
ImRaii.Tooltip()
```

### Example

```csharp
using var tooltip = ImRaii.Tooltip();
if (!tooltip) return;

// Draw the tooltip's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginTooltip()) {
    // Draw the tooltip's parts
    ImGui.EndTooltip();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
