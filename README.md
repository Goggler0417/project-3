# Tagmark v4.09

## Focus
Bookmark Tab visual restoration on top of the v4 engine.

## Added / changed
- Bookmark Tab now uses a v1-style panel: search/scope/sort/category row, result stats, action bar, selection bulk bar, stacked bookmark results.
- Bookmark Folder is rendered as a v1-style inline collapsible container. Unfiled bookmarks stay as normal cards rather than an artificial Unfiled folder.
- Bookmark cards are rendered by the existing Schema -> Field -> Placement engine. The visual appearance is not tied to Input names.
- Placement card settings: display format (title/link/info/meta/chips/record/notes/text/hidden), label mode, prefix/suffix, editor method.
- Field card layout: vertical or inline.
- v1 Bookmark and v2 Field one-click presets configure the same generic renderer; they are not separate data models.
- Tag Head display rule was added so the same Tag Input can be split into Artist/Series-like info lines and Remaining chips using Priority distribution.
- Search scope and temporary Category filter were restored for the Bookmark Tab.
- Existing v4.08 data is migrated once to a v1-style Bookmark presentation configuration. IDs and stored entity values are unchanged.
- Mobile layout retained and adapted for the restored Bookmark UI.

## Test data
A fresh DB still contains the `🧪 기능 테스트` Page. It includes Bookmarks, Tags, Tag Heads, Categories, Records, and a Folder. The test Bookmark schema receives the v1 preset after its sample Artist/Series heads are created.

## Testing
- JavaScript syntax check: performed.
- Headless Chromium smoke/click test: performed for Bookmark Tab render, v1/v2 preset switching, search scope, category quick filter, folder collapse, selection bulk bar, edit modal, and mobile viewport.
- Browser click testing used an in-memory IndexedDB stub because Chromium localhost access is blocked by administrator policy in this environment. Real IndexedDB persistence/reload was therefore not browser-tested here.
