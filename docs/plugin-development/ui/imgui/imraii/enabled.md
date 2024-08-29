# Enabled

This temporarily removes any [Disabled()](./disabled) effects.

```csharp
ImRaii.Enabled()
```

Both ImGui and ImRaii maintain a stack of disables such that to re-enable all of
the disables must be popped off the stack. This means that to have one enabled
item in teh midst of a group of disabled items one must pop all of the disables
(assuming some a nested) then re-push all of the disables. Generally one should
restructure their code to not require this but if you need this ability you can
use <code>Enabled()</code>.

**Note:** This method can only undo the actions of
<code>ImRaii.Disabled()</code> as only <code>ImRaii.Disabled()</code> tracks the
number of times it is called. This makes using this feature very brittle. If any
direct calls to <code> ImGui.BeginDisabled()</code> are made it will prevent
this method from re-enabling its code. Caution should be used when using this
method.

### Example

```csharp
bool flagThatMightSignalDisabled;
// ...
using (ImRaii.Disabled(flagThatMightSignalDisabled)) {
    // Draw the possibly disabled parts
    using (ImRaii.Enabled()) {
        // Some enabled parts
    }
    // Back to disabled
}
```
