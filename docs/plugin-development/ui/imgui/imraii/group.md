# Group

This starts a group component and then ends it when the block ends.

```csharp
ImRaii.Group()
```

### Example

```csharp
using var group = ImRaii.Group();
if (!group) return;

// Draw the group's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginGroup()) {
    // Draw the group's parts
    ImGui.EndGroup();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
