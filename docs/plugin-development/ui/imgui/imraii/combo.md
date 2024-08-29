# Combo

This starts a combo component and then ends it when the block ends.

```csharp
ImRaii.Combo(string label)
ImRaii.Combo(string label, string previewValue)
ImRaii.Combo(string label, string previewValue, ImGuiComboFlags flags)
```

<dl>
    <dt>label</dt>
    <dd>The label for this combo item. This can include an id suffix.</dd>
    <dt>previewValue</dt>
    <dd>String the show if an item has not been selected.</dd>
    <dt>flags</dt>
    <dd>The combo flags to apply to this child.</dd>
</dl>

### Example

```csharp
using var child = ImRaii.Combo("Language", "Select a language");
if (!child) return;

// Draw the child's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginCombo("Language", "Select a language")) {
    // Draw the combo's parts
    ImGui.EndCombo();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
