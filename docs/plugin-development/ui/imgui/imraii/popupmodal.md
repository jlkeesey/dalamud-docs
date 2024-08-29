# PopupModal

This starts a model popup window component and then ends it when the block ends.

```csharp
ImRaii.PopupModal(string id)
ImRaii.PopupModal(string id, ref bool open)
ImRaii.PopupModal(string id, ref bool open, ImGuiWindowFlags flags)
```

<dl>
    <dt>id</dt>
    <dd>The unique id of this popup.</dd>
    <dt>open</dt>
    <dd>A reference to a boolean that tracks whether this popup is open.</dd>
    <dt>flags</dt>
    <dd>The window flags to apply to this popup.</dd>
</dl>

### Example

```csharp
bool isOpen;
using var popup = ImRaii.PopupModal("popupId", ref isOpen, ImGuiWindowFlags.AlwaysAutoResize);
if (!popup) return;

// Draw the popup's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
bool isOpen;
if (ImGui.BeginPopupModal("popupId", ref isOpen, ImGuiWindowFlags.AlwaysAutoResize)) {
    // Draw the popup's parts
    ImGui.EndPopup();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
