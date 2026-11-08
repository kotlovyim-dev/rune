- **On Windows, a window that keeps changing no longer starves the app's other windows of paints.**
  After a change a window presents every refresh for a second, and it asked for each of those
  frames with `request_redraw` from inside its own `WM_PAINT`. Windows hands out `WM_PAINT` one
  window at a time, and a window that invalidates itself while painting is always the next one, so
  while a loop or a live value kept renewing the hold (a breathing mascot, a ticking clock) another
  window of the app opened white and never drew. The hold now takes its frames from the frame timer
  (`TIMER_FRAME`), which leaves the message queue empty between them.
