# Child

This starts a child window component and then ends it when the block ends.

```csharp
ImRaii.Child(string strId)
ImRaii.Child(string strId, Vector2 size)
ImRaii.Child(string strId, Vector2 size, bool border)
ImRaii.Child(string strId, Vector2 size, bool border, ImGuiWindowFlags flags)
```

<dl>
    <dt>strId</dt>
    <dd>The unique id of this child.</dd>
    <dt>size</dt>
    <dd>The size of this child.</dd>
    <dt>border</dt>
    <dd><code>true</code> if this child should draw a border.</dd>
    <dt>flags</dt>
    <dd>The window flags to apply to this child.</dd>
</dl>

### Example

```csharp
using var child = ImRaii.Child("childId", new Vector2(200.0f, 300.0f, true);
if (!child) return;

// Draw the child's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginChild("childId", new Vector2(200.0f, 300.0f, true)) {
    // Draw the child's parts
    ImGui.EndChild();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
