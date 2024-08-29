# TabBar

This starts a tab bar component and then ends it when the block ends.

```csharp
ImRaii.TabBar(string label)
ImRaii.TabBar(string label, ImGuiTabBarFlags flags)
```

<dl>
    <dt>label</dt>
    <dd>The id for this component.</dd>
    <dt>flags</dt>
    <dd>The tab bar flags from
    <a href="https://github.com/ImGuiNET/ImGui.NET/blob/master/src/ImGui.NET/Generated/ImGuiTabBarFlags.gen.cs">ImGuiTabBarFlags</a>.
    </dd>
</dl>

The individual tabs should be created using [TabBarItem](./tabbaritem).

### Example

```csharp
using var tabbar = ImRaii.TabBar("tabbarId");
if (!tabbar) return;

// Draw the tabbar's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginTabBar("tabbarId")) {
    // Draw the tabbar's parts
    ImGui.EndTabBar();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
