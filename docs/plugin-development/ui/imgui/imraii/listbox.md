# ListBox

This starts a list box component and then ends it when the block ends.

```csharp
ImRaii.ListBox(string label)
ImRaii.ListBox(string label, Vector2 size)
```

<dl>
    <dt>label</dt>
    <dd>The label for this component.</dd>
    <dt>size</dt>
    <dd>The size for this component.</dd>
</dl>

### Example

```csharp
using var listbox = ImRaii.ListBox("List of things");
if (!listbox) return;

// Draw the listbox's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginListBox()) {
    // Draw the listbox's parts
    ImGui.EndListBox();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
