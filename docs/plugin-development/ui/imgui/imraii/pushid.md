# PushId

This sets the id for the next created object and then resets it when the block
ends.

```csharp
ImRaii.PushId(string id, bool condition = true)
ImRaii.PushId(int id, bool condition = true)
ImRaii.PushId(IntPtr id, bool condition = true)
```

<dl>
    <dt>id</dt>
    <dd>The id to push. This can be a string, an integer, or an <code>IntPtr</code>.</dd>
    <dt>condition</dt>
    <dd>An optional condition value. If this value is <code>false</code>, then
    this id setting does not take place.</dd>
</dl>

### Example

```csharp
using (ImRaii.PushId("anId")) {
    // Do some stuff
}
```

### Replaces

```csharp
if (ImGui.PushId("anId")) {
    // Do some stuff

    ImGui.PopId();
}
```
