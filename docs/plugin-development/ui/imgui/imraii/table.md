# Table

This starts a table component and then ends it when the block ends.

```csharp
ImRaii.Table(string table)
ImRaii.Table(string table, int numColumns)
ImRaii.Table(string table, int numColumns, ImGuiTableFlags flags)
ImRaii.Table(string table, int numColumns, ImGuiTableFlags flags, Vector2 outerSize)
ImRaii.Table(string table, int numColumns, ImGuiTableFlags flags, Vector2 outerSize, float innerWidth)
```

<dl>
    <dt>table</dt>
    <dd>The id for this table.</dd>
    <dt>numColumns</dt>
    <dd>The number of columns in this table.</dd>
    <dt>flags</dt>
    <dd>The flags for this table from <code>ImGuiTableFlags</code>.</dd>
    <dt>outerSize</dt>
    <dd>The outer size for this table.</dd>
    <dt>innerWidth</dt>
    <dd>The horizontal size of the interior values (columns) display area. If
    this is 0.0f then the interior takes up the size of the table. IF this is
    any other value, then the interior will be that size. If the size is larger
    than the visible are then horizontal scrolling will be enabled.</dd>
</dl>

### Example

```csharp
using var table = ImRaii.Table("tableId", 3);
if (!table) return;

// Draw the table's parts
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginTable("tableId", 3)) {
    // Draw the table's parts
    ImGui.EndTable();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
