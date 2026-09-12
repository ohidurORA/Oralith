Continue working on the existing Oralith repository.

This is a refinement pass for the already-implemented Notes experience. Do NOT redesign the entire application or replace working functionality unnecessarily.

Before changing UI code, re-read and obey the project `skills/` directory and all relevant design/animation guidance. The existing design language remains the authority.

The goal of this task is to fix the remaining Notes-editor issues and add the missing interactions described below.

# 1. NOTE EDITOR — REMOVE THE EXCESSIVE TOP SPACE

When opening an existing note or creating a new note, the editor currently has a very large empty area above the editor content.

That vertical gap appears to be inherited from the Notes home screen header containing:

- Oralith
- Notes / To-do tabs

The editor must NOT reserve space for that previous home-screen header.

The note editor should start naturally near the top of the screen using proper system-bar/edge-to-edge insets only.

Do NOT copy the Notes-home header spacing into the editor.

The editor should feel compact, intentional, and immediately usable.

## Desired top structure

The editor should have one compact top bar containing:

- back/navigation
- editable note title
- undo
- redo
- share/export actions

There should NOT be a giant blank region above it.

# 2. REMOVE THE SECOND / SEPARATE TITLE FIELD

There is currently an additional title section below the upper editor bar.

Remove that separate title field.

The note title must exist directly in the top editor bar.

The title should appear on the same horizontal level as the undo/redo/share/export controls.

The user should be able to tap the visible title directly and edit it.

For a new note, show:

`Untitled`

as the default title.

When the user taps the title:

- it becomes editable
- the keyboard appears appropriately
- editing should not cause the entire UI to jump unnecessarily
- the title should remain visually integrated with the top bar

When the user finishes editing, keep the title in the same location.

Do not create a second title input lower in the document.

# 3. TOP BAR SPACING AND ALIGNMENT

The editor top bar should have a professional, compact hierarchy.

Requirements:

- no unnecessary giant vertical margins
- no duplicated headers
- correct status-bar inset
- balanced spacing between title and actions
- title should have enough width to remain readable
- undo/redo should remain accessible
- export/share controls should remain accessible
- smaller screens must not cause controls to overlap

If there is not enough horizontal room, use a secondary menu for low-priority actions rather than allowing the layout to break.

Follow the repository's typography, spacing, material, and interaction guidance.

# 4. MEDIA RESIZE — PRESERVE ASPECT RATIO

Images, videos, and other visual media currently support resizing, which is good. Improve the resizing behavior.

The media element must preserve its natural aspect ratio by default.

If the user drags a resize handle:

- changing width should proportionally change height
- changing height should proportionally change width
- the media must never become absurdly thin or stretched by accidental resizing
- the aspect ratio must remain stable unless an intentional future crop/free-transform feature is introduced

Do NOT allow arbitrary width-only or height-only squashing.

Example:

If an image is originally 16:9 and the user makes it narrower, it should automatically become proportionally shorter.

If the user makes it wider, it should automatically become proportionally taller.

# 5. MEDIA MINIMUM SIZE / RESIZE LIMIT

Add sensible minimum and maximum dimensions.

The minimum size should be determined relative to:

- original aspect ratio
- available editor width
- usable touch target
- screen density
- media type

The resize system should prevent the user from reducing a media object to a visually useless sliver.

Do not hardcode one universal minimum width that looks correct only on one device.

The minimum bounds should respect the element's aspect ratio.

Similarly, prevent a media object from expanding beyond sensible document/editor bounds.

# 6. RESIZE EXPERIENCE

Keep the existing media resize handle/interaction because the visual concept is good.

However:

- make the resize handle/track slightly smaller
- keep it easy to discover
- keep it easy to touch
- reduce unnecessary visual bulk
- maintain a polished appearance

The resize affordance should feel like part of the media element, not a giant control bar.

During resizing:

- update the media continuously
- keep the interaction directly tied to the user's finger
- avoid lag
- avoid snapping unexpectedly
- use appropriate spring/gesture behavior after release where relevant
- preserve aspect ratio continuously

Follow the repository animation skills for direct manipulation, interruptibility, and smooth gesture handling.

# 7. AUDIO PLAYER — ADD SCRUBBING

The audio media block currently cannot be scrubbed correctly.

Fix this.

Audio should have a seek/scrub control equivalent in behavior to the existing video scrubbing experience.

The user must be able to:

- drag the progress position
- tap the progress position where appropriate
- seek accurately
- see current progress
- see total duration
- resume playback from the selected position

The interaction should feel as polished as the existing video scrubber.

Do not make audio seeking depend on stopping and restarting playback unnecessarily.

Use a proper media playback architecture rather than manually faking a progress bar.

# 8. AUDIO / VIDEO / IMAGE MEDIA HANDLE SIZE

All media elements currently have a compact bar/handle-like interaction area used for resizing or manipulation.

Keep this interaction.

However, reduce its physical size slightly.

Requirements:

- still easy to touch
- visually subtle
- not excessively tall
- consistent across image/video/audio media where applicable
- does not dominate the content

Do not make it so small that it becomes difficult to operate on a phone.

Follow accessibility/touch-target requirements even while making the control visually compact.

# 9. LONG-PRESS MEDIA SELECTION / DELETION

Implement a proper long-press action for every media type:

- image
- video
- audio

When the user long-presses a media block:

1. Select the media block.
2. Clearly indicate that it is selected.
3. Reveal a contextual Delete action.

The Delete action may appear:

- in the editor's contextual toolbar
- or in the top action area

Choose whichever fits the existing design language best.

Do NOT require the user to open an unrelated settings menu.

The delete action must remove the media from the document structure and correctly clean up its local media reference/storage when safe to do so.

Do not accidentally delete the user's source media from the device's general media library unless the user explicitly requested that behavior.

Deleting the media from a note should mean:

"remove it from this note"

not:

"delete the original file from the phone."

Undo should restore the removed media where technically possible.

# 10. MEDIA SELECTION STATE

Selected media should have a clear but elegant selection state.

Use:

- subtle outline
- restrained background/accent
- appropriate handles
- clear context action

Do not use aggressive red styling merely because Delete is available.

Red should primarily communicate destructive action, not dominate the entire selected media element.

# 11. MEDIA IMPORT — USE THE PHONE'S MEDIA LIBRARY

The current import experience behaves more like a generic local file browser.

Change the default media-import workflow.

The Notes editor should request and use the appropriate Android media permissions/access mechanisms and access the device's local media library.

The user should be able to browse/import:

- images
- videos
- audio

from the phone's available media.

The experience should be designed around an in-app Oralith media library UI where practical.

Do NOT build an unnecessary imitation of Android's complete system file manager.

Use Android's modern media/storage APIs correctly for the supported Android versions.

Where Android requires a permission, request the minimum appropriate permission at the appropriate moment.

Do NOT request permissions at application startup simply because the feature exists.

Ask for access when the user actually invokes media import.

# 12. MEDIA PERMISSION HANDLING

Handle all permission states properly:

- permission granted
- permission denied
- partially granted / limited access where applicable
- permission permanently denied
- no compatible media available

The UI should explain what access is needed and why.

Do not crash when permission is denied.

Do not show an empty broken media browser.

Provide a graceful fallback to an appropriate system picker when platform behavior requires it.

The app remains local-first and must not upload media anywhere.

# 13. BULLET LISTS — DELETION MUST WORK

There is already a list/bullet feature.

Creating a list item and pressing Enter correctly creates the next chronological item.

Keep that behavior.

Fix deletion.

The user must be able to remove list items naturally using:

- Backspace
- Delete
- removing the item's content and continuing backward
- normal cursor editing behavior

When the user deletes an empty list item, the list marker itself must be removed appropriately.

Example:

`• Item`

Backspace at the beginning/empty state should not leave an invisible bullet that cannot be removed.

The user should be able to exit a list naturally by deleting/backspacing an empty list item according to standard editor behavior.

Do not leave orphaned bullet/list metadata behind.

Undo must restore the previous list state.

# 14. TABLE CREATION FEATURE

Add a table-creation tool to the editor toolbar.

The toolbar should contain a:

`Table`

or

`Create Table`

action.

When selected, reveal a secondary control area consistent with the existing formatting/bullet tool interaction.

The user should be able to specify:

- number of rows
- number of columns

Then confirm/create the table.

For example:

Rows: 4
Columns: 3

Confirm → insert table at the current cursor/document position.

The table must belong to the document model, not be a screenshot or flattened visual object.

# 15. TABLE INITIAL APPEARANCE

Tables should initially look polished and balanced.

Requirements:

- reasonable width
- generous but not excessive height
- readable cell padding
- clear row/column separation
- consistent typography
- proper alignment
- enough space for text editing
- visually consistent with Oralith

Do not create extremely tiny cells.

Do not make every table automatically consume the entire screen vertically.

The table should adapt to the editor width.

# 16. TABLE EDITING

The table must be editable after creation.

Users should be able to tap cells and type content normally.

The document model must preserve:

- rows
- columns
- cell contents
- row sizes
- column sizes
- formatting where supported

Do not flatten the table into an image.

# 17. TABLE ROW / COLUMN RESIZING

Users must be able to resize individual table boundaries.

For horizontal boundaries:

- drag the boundary vertically to change row height

For vertical boundaries:

- drag the boundary horizontally to change column width

The important behavior is:

A user's adjustment should affect the specific boundary being moved.

Do NOT automatically redistribute all other boundaries unless required by minimum constraints.

Example:

Suppose the table width is conceptually 100 units.

A vertical divider is currently at 20.

The user drags it to 30.

The divider should move to 30.

The neighboring region should adapt as necessary, but unrelated dividers should retain their current positions wherever possible.

Do not squash every other column just because one boundary moved.

# 18. INDEPENDENT TABLE BOUNDARIES

Treat row/column boundaries as independent editable positions.

Do not implement resizing by blindly assigning equal fractions after every drag.

Persist boundary positions or proportions in the document model.

Respect:

- minimum cell size
- maximum usable size
- table bounds
- device width
- text scaling

The result should resemble a professional design/layout tool rather than a basic static Android TableLayout.

# 19. TABLE RESIZE GUIDES

When the user begins dragging a row or column boundary, show a temporary floating measurement indicator directly near the active boundary.

The indicator should communicate the current position/proportion/measurement.

For example:

`30%`

or an appropriate width measurement.

The indicator should appear only while the boundary is actively being adjusted.

When the user stops dragging or taps elsewhere:

- hide the measurement indicator
- leave the table in its new state

Do not permanently display measurement labels across the whole table.

# 20. TABLE RESIZE INTERACTION

Boundary dragging must be:

- direct
- smooth
- continuous
- interruptible
- responsive to the finger

The boundary should track the user's drag rather than jumping toward a target.

Respect the repository's gesture/animation design rules.

Do not use unnecessary fixed-duration animations during active dragging.

# 21. TABLE TOUCH TARGETS

Visual boundary lines may be thin.

Their interactive touch region should be larger than their visible line.

This is important for phones.

The user should not have to precisely touch a one-pixel line.

Use invisible hit padding around resize boundaries while keeping the visible UI elegant.

# 22. TABLE CONSTRAINTS

Prevent invalid tables.

Never allow:

- zero-width columns
- zero-height rows
- negative dimensions
- cells too small to interact with
- table overflow outside the usable document area

Apply sensible minimum constraints.

Do not let one resize gesture destroy the usability of the entire table.

# 23. DOCUMENT MODEL UPDATE

Extend the existing document structure cleanly to support tables.

Tables should be first-class document content.

Do not store them as arbitrary JSON fragments without a defined model.

Maintain versionable serialization.

Existing notes created before this update must remain readable.

Do not break old documents.

# 24. TOOLBAR INTEGRATION

Integrate the Table action into the existing bottom editor tool system.

The interaction should feel consistent with:

- bullets
- formatting
- font
- text size
- media insertion

When Table is selected, show the table-specific controls without permanently occupying large screen space.

Do not create a completely different UI paradigm for tables.

# 25. ERROR-SAFE INTERACTIONS

All of the new interactions must fail gracefully.

Examples:

- media permission denied
- unsupported media
- failed playback
- failed media import
- failed deletion
- invalid table dimensions
- export/document incompatibility
- corrupted document data

Never crash the application because the user selected an invalid or unsupported media/document operation.

# 26. PERFORMANCE

Do not degrade the existing performance of the editor.

Media resizing must not trigger expensive full-document recomposition unnecessarily.

Audio progress updates must be efficient.

Table dragging must remain smooth.

Avoid recomputing the entire document model for every drag frame.

Use stable keys and appropriate state architecture.

Do not put expensive processing directly inside composables.

# 27. PERSISTENCE

Every new feature must persist correctly.

Persist:

- media dimensions
- media aspect ratio
- media placement/layout state
- list state
- table structure
- row sizes
- column sizes
- table contents
- selected formatting where applicable

Do not persist transient UI state unnecessarily, such as:

- active resize measurement overlay
- temporary selection highlight
- temporary permission dialogs

# 28. UNDO / REDO INTEGRATION

All structural editing actions should integrate with the existing undo/redo system.

At minimum:

- media resize
- media deletion
- list item deletion
- table insertion
- table cell edits
- row resizing
- column resizing

should participate appropriately in undo/redo.

Do not create separate incompatible histories.

# 29. DESIGN REVIEW

After implementing these changes, review the entire editor against the project's `skills/` directory again.

Pay particular attention to:

- excessive spacing
- hierarchy
- typography
- gesture responsiveness
- direct manipulation
- spring/settling behavior
- bottom toolbars
- selection states
- overlays
- contextual actions
- accessibility
- reduced motion
- touch targets
- responsive behavior

Remove anything that feels visually excessive.

The result should feel like one coherent, premium editor.

# 30. DO NOT BREAK EXISTING FEATURES

Before finishing, verify that the following existing behavior still works:

- create note
- open note
- edit title
- edit text
- save locally
- reopen after restart
- undo
- redo
- insert image
- insert video
- insert audio
- resize media
- play media
- export behavior
- bottom navigation
- Notes/To-do tabs
- empty Clock page
- empty Calculator page

Do not rewrite working systems unnecessarily.

# 31. FINAL VERIFICATION

After implementation:

1. Build the application.
2. Run relevant tests.
3. Verify the editor on a small phone-sized layout.
4. Verify it on a larger screen.
5. Verify portrait and landscape where practical.
6. Verify larger system font sizes.
7. Test media resizing at minimum and maximum bounds.
8. Test audio seeking.
9. Test long-press media deletion.
10. Test list-item deletion.
11. Test table creation.
12. Test table cell editing.
13. Test independent row resizing.
14. Test independent column resizing.
15. Test measurement overlay appearance/disappearance.
16. Test undo/redo for the new structural operations.
17. Test permission-denied media import behavior.

Fix issues discovered during verification before declaring the work complete.

IMPORTANT:

Do not implement these features as fake visual demonstrations.

They must be backed by the actual document model, persistence system, and correct Android interaction behavior.

Do not silently lose user data.

Do not delete original phone media when the user only removes it from a note.

Do not introduce unnecessary dependencies.

Do not compromise the existing Oralith design language.