# ImRaii

ImRaii is a Dalamud provided library that simplifies interacting with ImGui.
Every plugin should use ImRaii's methods when possible as they will make it much
more difficult to make mistakes.

As mentioned elsewhere, it is imperative that ImGui `Begin` / `End` and `Push` /
`Pop` calls match. Failure to do so will cause all kinds or weird behavior in
the UI. But, one of the big problems is that the closing call must only be made
if the opening call succeeds. But, not all of the matching calls have a succeeds
flag (e.g. `ImGui.PushStyleColor`) they also tend to come in sequences e.g. set
some colors, the font, and maybe the width. ImRaii helps with all of that.

The basic idea behind ImRaii is that it creates `IDisposable` objects on the
opening calls that you hand to a `using` statement that guarantees that the
closing call happens even in the face of exceptions. There are two basic
patterns to use. The first is for the calls that do not have a succeeds flag and
the second for those that do.

The first pattern for those calls that always succeed is this:

```csharp
using (ImRaii.PushColor(ImGuiCol.Text, 0xff0000ff)) {
    // Do some stuff
}
```

This will set the text color to red and then after the code is done, will pop
the color, resetting it to its previous value.

The second pattern is for calls that may not succeed. Succeed in this case
refers to ImGui determining that it should be displayed at this time.

```csharp
using (var listbox = ImRaii.ListBox("##listboxid"))
if (listbox) {
    // Add listbox items
}
```

As an alternative, if you place such blocks in their own functions (which you
should), then you can use this form which help reduce nesting:

```csharp
public void DrawListbox()
{
    using var listbox = ImRaii.ListBox("##listboxid");
    if (!listbox) return;

    // Add listbox items
}
```

The remainder of this section contains usage for all of the helpers that ImRaii
provides. These are not complete descriptions of all of the possible variations
of these helper, but a general description of how to use the helpers and which
`using` pattern to use.
