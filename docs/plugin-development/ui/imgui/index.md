# ImGui

The UI for plugins is built using [ImGui](https://github.com/ocornut/imgui).
This library is a little different from most you may have worked with and there
are a few points to keep in mind:

- Your rendering code is run every frame. This means that you should not do
  major calculations in the drawing code. Most normal stuff is fine, but don't
  try to calculate the 1,000,000<sup>th</sup> digit of &pi;.
- If there is a `Begin` or `Push` method it **must** be matched with the
  corresponding `End` or `Pop` call. Not matching the calls will cause all kinds
  of headaches. See [ImRaii](imraii) for more information and utilities to help
  with this.
- The ImGui windows generally sit on top of the game window and are used to set
  and collect information that is extra to the game. If you wish to modify the
  actual game windows and menus that is using a completely different system see
  [Atk](../atk)
