# TreeNode

This starts a tree node component and then ends it when the block ends.

```csharp
ImRaii.TreeNode(string label)
ImRaii.TreeNode(string label, ImGuiTreeNodeFlags flags)
```

<dl>
    <dt>label</dt>
    <dd>The label for this component.</dd>
    <dt>flags</dt>
    <dd>The tree node flags from
    <a href="https://github.com/ImGuiNET/ImGui.NET/blob/master/src/ImGui.NET/Generated/ImGuiTreeNodeFlags.gen.cs">ImGuiTreeNodeFlags</a>.
    </dd>
</dl>

### Example

```csharp
using var treenode = ImRaii.TreeNode("Top Level");
if (!treenode) return;

using (var treenode2 = ImRaii.TreeNode("1st Level - Intro"))
if (treenode2) {
    // Draw the treenode2's parts
}

using (var treenode3 = ImRaii.TreeNode("1st Level - Boxes"))
if (treenode3) {
    // Draw the treenode3's parts
}
```

### Replaces

This helper replaces this ImGui code:

```csharp
if (ImGui.BeginTreeNode("Top Level")) {
    if (ImGui.BeginTreeNode("1st Level - Intro")) {
        // Draw the treenode2's parts
    }
    if (ImGui.BeginTreeNode("1st Level - Boxes")) {
        // Draw the treenode3's parts
    }
    ImGui.EndTreeNode();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
