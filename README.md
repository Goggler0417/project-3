# Tagmark v4.25

## Changes
- Replaced manual up/down ordering controls with pointer-based drag & drop for Field/Placement, Tabs, and Tag Heads.
- Converted visible button labels containing “추가” to compact `＋` buttons while retaining descriptive title/aria labels.
- Moved new-tab creation out of Page Settings; a `＋` button now sits beside the page tabs and opens the New Tab modal.
- Reworked Page Settings tab rows for aligned drag handle, editable name, duplicate, and delete controls.
- Removed the generic AND/OR filter-combination system and simplified general/category filters to one condition.
- Tag creation now allows zero Tag Heads selected. Headless Tags are shown under a dynamic `미지정` group, which disappears automatically when no headless Tags remain.
- Added/kept pointer-event drag UI designed to work across mouse, trackpad, and touch.
- Fixed the advanced schema rule visibility handler and cleaned obsolete reorder helpers.

## QA
- JavaScript syntax check passed after extracting the inline script.
- Duplicate named function declarations: 0.
- Native `prompt` / `alert` / `confirm`: 0.
- HTML `draggable=` usage: 0.
- Visible up/down reorder buttons: 0.
- Visible buttons containing `추가`: 0.
- Generic `filterJoin`, `categoryRules`, `op:'and'`, `op:'or'`: 0.
- Runtime QA previously verified Tab and Tag Head pointer reordering and headless Tag `미지정` appearance/disappearance.
- 390px mobile horizontal-overflow QA passed in the test harness.

Note: the existing Bookmark comma-separated multi-term search is unchanged; it is search behavior, not the removed generic AND/OR filter combinator.
