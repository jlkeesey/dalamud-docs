# TabBarItem

This starts a tab bar panel component and then ends it when the block ends.

```csharp
ImRaii.TabBarItem(string label)
ImRaii.TabBarItem(string label, ref bool open)
ImRaii.TabBarItem(string label, ImGuiTabItemFlags flags)
ImRaii.TabBarItem(string label, ref bool open, ImGuiTabItemFlags flags)
ImRaii.TabBarItem(byte* byteLabel, ImGuiTabItemFlags flags)
```

<dl>
    <dt>label</dt>
    <dd>The label for this tab.</dd>
    <dt>open</dt>
    <dd>A ref bool that is set to <code>false</code> when the tab is closed.</dd>
    <dt>byteLabel</dt>
    <dd>The label for this tab as a <code>byte*</code>. Not used in normal cases.</dd>
    <dt>flags</dt>
    <dd>The tab bar item flags from
    <a href="https://github.com/ImGuiNET/ImGui.NET/blob/master/src/ImGui.NET/Generated/ImGuiTabItemFlags.gen.cs">ImGuiTabItemFlags</a>.
    </dd>
</dl>

This tab must be created in the context of a [TabBar](./tabbar).

### Example

```csharp
using var tabbar = ImRaii.TabBar("tabbarId");
if (!tabbar) return;

using (var tab1 = ImRaii.TarBarItem("First", ImGuiTabItemFlags.Selected))
if (tab1) {
    // Draw tab1 parts
}

using (var tab2 = ImRaii.TarBarItem("Second"))
if (tab2) {
    // Draw tab2 parts
}
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginTabBar("tabbarId")) {
    if (ImGui.BeginTabBarItem("First", ImGuiTabItemFlags.Selected)) {
        // Draw tab1 parts
        ImGui.EndTabBarItem();
    }
    if (ImGui.BeginTabBarItem("Second")) {
        // Draw tab2 parts
        ImGui.EndTabBarItem();
    }
    ImGui.EndTabBar();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
