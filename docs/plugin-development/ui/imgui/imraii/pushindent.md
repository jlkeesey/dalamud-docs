# PushIndent

This sets the indent for the next created object and then resets it when the
block ends.

```csharp
ImRaii.PushIndent(float f, bool scaled = true, bool condition = true)
ImRaii.PushIndent(int i = 1, bool condition = true)
```

<dl>
    <dt>f</dt>
    <dd>The amount of indent to add using ImGui coordinates. If this number is
    negative, then this subtracts from the indent.</dd>
    <dt>scaled</dt>
    <dd>If <code>true</code> apply the current Dalamud window scaling factor.</dd>
    <dt>i</dt>
    <dd>The multiplier for the <code>IndentSpacing</code> ImGui style. IF this
    is negative then the value is subtracted from the indent.</dd>
    <dt>condition</dt>
    <dd>An optional condition value. If this value is <code>false</code>, then
    the indent is not changed.</dd>
</dl>

### Example

```csharp
using (ImRaii.PushIndent(50.0f, true)) {
    // Do some stuff
}
```

```csharp
using (ImRaii.PushIndent(50.0f, true, flagDeterminingIfWeShouldIndent)) {
    // Do some stuff
}
```

### Replaces

```csharp
var indentation = 50.0f * ImGui.GetStyle().IndentSpacing;
// ...
ImGui.Indent(indentation);
// Do some stuff
ImGui.Unindent(indentation);
```

```csharp
var indentation = 50.0f * ImGui.GetStyle().IndentSpacing;
// ...
if (flagDeterminingIfWeShouldIndent) ImGui.Indent(indentation);
// Do some stuff
if (flagDeterminingIfWeShouldIndent) ImGui.Unindent(indentation);
```
