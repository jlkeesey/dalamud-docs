# ContextPopupItem

This starts a context popup window component and then ends it when the block
ends.

```csharp
ImRaii.ContextPopupItem(string id)
ImRaii.ContextPopupItem(string id, ImGuiPopupFlags flags)
```

<dl>
    <dt>id</dt>
    <dd>The unique id of this popup.</dd>
    <dt>flags</dt>
    <dd>The popup flags to apply to this popup.</dd>
</dl>

### Example

```csharp
using var popup = ImRaii.ContextPopupItem("popupId");
if (!popup) return;

// Draw the popup's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
bool isOpen;
if (ImGui.BeginPopupContextItem("popupId")) {
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
