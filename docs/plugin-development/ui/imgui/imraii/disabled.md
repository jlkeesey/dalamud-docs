# Disabled

This marks the following ImGui items as disabled and then ends it when the block
ends.

```csharp
ImRaii.Disabled()
ImRaii.Disabled(bool disabled)
```

<dl>
    <dt>disabled</dt>
    <dd><code>true</code> if this child should disabled, otherwise nothing
    changes.</dd>
</dl>

Both ImGui and ImRaii maintain a stack of disables such that to re-enable all of
the disables must be popped off the stack. This means that to have one enabled
item in teh midst of a group of disabled items one must pop all of the disables
(assuming some a nested) then re-push all of the disables. Generally one should
restructure their code to not require this but if you need this ability see
[Enabled()](./enabled).

### Example

```csharp
bool flagThatMightSignalDisabled;
// ...
using (ImRaii.Disabled(flagThatMightSignalDisabled)) {
    // Draw the possibly disabled parts
}
```

### Replaces

This helper replaces this ImGui code:

```csharp
bool flagThatMightSignalDisabled;
// ...
if (flagThatMightSignalDisabled && ImGui.BeginDisabled()) {
    // Draw the possibly disabled parts
    if (flagThatMightSignalDisabled) ImGui.EndDisabled();
}
```

But the ImRaii works correctly in case of an exception.

### Note

Be sure to check the <code>IDisposable</code> object and only draw the parts if
the value is <code>true</code>. If the value is <code>false</code> then the
object is not being drawn and any part rendering code will be drawn correctly if
at all.
