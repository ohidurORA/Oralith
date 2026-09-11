You have access to my GitHub repository:

`https://github.com/ohidurORA/Oralith`

Work directly from the existing repository and treat the current project as the starting template, not as disposable example code.

# ORALITH — MASTER DEVELOPMENT INSTRUCTION

Build Oralith as a polished, production-quality, local-first Android application.

The current repository is only the initial Android Studio/Jetpack Compose template. Before implementing features, inspect the entire repository and understand the existing Gradle setup, package structure, theme files, resources, tests, and especially the complete `skills/` directory.

## 1. ABSOLUTE UI DESIGN RULE

This is the highest-priority rule in the entire project.

Before designing, implementing, modifying, or reviewing ANY UI, you MUST read and apply ALL relevant files inside:

`/skills/`

Read the entire directory recursively, not just one file.

The skill files are design and implementation authority for this project. In particular, use the supplied Apple-design, animation, animation-vocabulary, UI-library-selection, prototyping, animation-review, animation-improvement, and other design-engineering guidance wherever applicable.

Do not selectively follow only the parts that are convenient.

After implementation, audit the resulting UI code against the supplied skills and correct violations.

The final UI should feel coherent, premium, restrained, responsive, deliberate, and highly polished rather than like a collection of default Material components.

Do not blindly imitate Apple's visual identity or copy proprietary interfaces. Use the supplied design principles—fluidity, spatial consistency, hierarchy, restraint, typography, material depth, responsiveness, and interaction quality—to create an original Oralith design language.

## 2. TECHNOLOGY RULE

Primary language:

- Kotlin

UI:

- Jetpack Compose
- Compose Material 3 where appropriate
- Compose-native custom components where necessary

Architecture/business/data logic:

- Kotlin
- AndroidX architecture components
- ViewModel/state-holder architecture
- Repository pattern
- Room for persistent local data

Do NOT use C++ for normal application logic.

Only introduce native code when there is a demonstrated, measurable requirement that cannot reasonably be handled by Kotlin/Android APIs. Do not add native complexity prematurely.

Important clarification:

Jetpack Compose is the UI technology, not the backend.

Therefore:

- UI = Jetpack Compose
- application/domain/data logic = Kotlin
- local database = Room
- local files/media storage = Android storage APIs
- audio/video playback = an appropriate Android media stack such as Media3 when justified

Keep dependencies lightweight and purposeful.

Do not add large libraries simply because they are convenient.

## 3. PERFORMANCE PRINCIPLE

Oralith must be designed to run extremely well across a very broad range of Android phones, including low-end and older devices.

Prioritize:

- fast startup
- low memory usage
- low unnecessary CPU usage
- smooth scrolling
- minimal recomposition
- efficient persistence
- efficient image loading
- efficient media playback
- lazy lists/grids where appropriate
- avoiding unnecessary background work
- avoiding unnecessary dependencies
- avoiding giant in-memory document representations
- avoiding blocking the main thread
- avoiding expensive work inside composables

Everything should be asynchronous where appropriate.

Never perform database, file, media, export, decoding, or other expensive work directly on the UI thread.

Do not sacrifice correctness or UX merely to make the code shorter.

## 4. LOCAL-FIRST / PRIVACY RULE

Oralith is 100% local-first.

The application must work without an account and without requiring cloud services.

Notes, document state, metadata, imported media, preferences, and other user-created content should remain on-device unless the user explicitly exports or shares something.

Do not introduce analytics, telemetry, remote synchronization, unnecessary network access, or cloud dependencies.

For fonts, icons, and other static resources, prefer bundling them into the application rather than downloading them dynamically at runtime.

## 5. INFORMATION ARCHITECTURE

The main Oralith application has three primary bottom destinations:

1. Notes
2. Clock
3. Calculator

Notes is the only functional area to implement now.

Clock and Calculator should exist architecturally but remain intentionally empty until their implementation phase.

Inside Notes there are two top-level tabs:

- Notes
- To-do

Notes is selected by default.

For now:

- Notes = functional
- To-do = empty placeholder
- Clock = empty placeholder
- Calculator = empty placeholder

Do not partially implement Clock or Calculator.

Do not create fake functionality simply to make those pages look complete.

## 6. REQUIRED PROJECT STRUCTURE

The project must have a clean, scalable, feature-oriented package structure.

Do NOT place the entire application inside `MainActivity.kt`.

Create separate files for separate responsibilities and separate screens.

Use a structure conceptually similar to:

`com.ora.oralith`

- `core/`
  - shared utilities
  - common UI infrastructure
  - storage helpers
  - media helpers
  - export helpers
  - constants where appropriate

- `data/`
  - database
  - entities
  - DAOs
  - repositories
  - local storage

- `domain/`
  - document models
  - editor models
  - use cases
  - export models
  - business rules

- `ui/`
  - app
  - navigation
  - theme
  - components
  - common

  - `notes/`
    - notes home screen
    - notes tab
    - to-do tab
    - note editor
    - media components
    - formatting UI
    - import browser
    - export UI
    - note-specific state

  - `clock/`
    - folder/package exists
    - page placeholder only

  - `calculator/`
    - folder/package exists
    - page placeholder only

Use additional subfolders/files when a feature is complex.

The exact names may be improved by you, but maintain the same principle:

ONE RESPONSIBILITY = ONE APPROPRIATE FILE/COMPONENT.

Do not create giant 1000+ line composables when the UI can reasonably be decomposed.

## 7. MAIN APPLICATION SHELL

Create a professional application shell.

The top-level visual identity should use:

- rich modern black
- white
- sophisticated shades/tints/hues of blue

Use blue intentionally for hierarchy, interactive states, accents, selection, focus, links, and meaningful feedback.

Do not make everything blue.

Do not use excessive gradients.

Do not make the interface visually noisy.

The design should feel luxurious, modern, clean, intelligent, and restrained.

Use appropriate dark/light theme behavior if the existing theme architecture supports it, but maintain Oralith's brand identity across themes.

Use proper system bar handling and edge-to-edge layout.

Respect accessibility and dynamic font scaling.

## 8. BOTTOM NAVIGATION

The main application has a bottom navigation area with:

Notes | Clock | Calculator

Notes is selected initially.

Use high-quality, consistent icons.

Prefer a reliable icon system/library that provides visually coherent vector icons.

Do not use random emoji as icons.

Use Material Symbols/Compose icon resources or another lightweight, reliable vector icon source when appropriate.

Use custom vector artwork only when a required icon genuinely cannot be represented well by the selected icon system.

Every icon must have an obvious semantic purpose and appropriate accessibility description.

## 9. NOTES HOME SCREEN

At the top:

Left:

`Oralith`

Right:

a two-option Notes/To-do segmented/tab control.

Default selected tab:

`Notes`

The Notes tab should present existing notes in a polished, efficient list/grid arrangement that can evolve later.

Do not overdesign an empty state.

The empty state should be useful, visually balanced, and consistent with the design system.

Provide a prominent but elegant add-note control.

The primary add button should be a circular floating action control positioned above the bottom navigation area, respecting gesture/navigation insets.

Use the supplied animation skills for its appearance, press feedback, and transitions.

## 10. NOTE CREATION / EDITOR

Selecting the add button opens the note editor as a proper screen, not a crude popup.

The editor needs:

- title field
- body/content editor
- scrolling content area
- multilingual text input
- undo
- redo
- automatic local persistence
- explicit save behavior where useful
- export controls
- media insertion
- formatting controls

Users must be able to type arbitrary Unicode text and multiple languages.

Do not assume English-only input.

The title and document body should be separate logical fields.

The document must survive process death and application restart.

Auto-save should be efficient and not write to Room on every individual keystroke.

Use a sensible debounced/pending-save strategy while ensuring that user data is not easily lost.

## 11. DOCUMENT MODEL

Do not represent the complete rich document as one uncontrolled string.

Use a document model that can support structured content.

Design the model so it can represent things such as:

- paragraphs
- text spans
- headings
- bold
- italic
- underline
- text color
- font
- text size
- links
- bullet lists
- media blocks
- media metadata
- block positioning/layout metadata where needed

The storage representation should be versionable so future Oralith features can evolve without corrupting old documents.

A JSON/blob representation inside a Room entity may be appropriate for complex editor state, provided the architecture remains maintainable and efficient.

Do not put binary media directly into Room unless there is a compelling reason.

Store actual media in application-managed local storage and keep metadata/reference information in Room.

## 12. MEDIA SUPPORT

The note editor must support inserting:

- images
- video
- audio

Media must appear as actual interactive content inside the note.

Users should be able to:

- insert media
- reposition media where supported
- resize media
- interact with media
- play audio
- play video
- view images

Media cards/tiles must visually belong to the document instead of looking like raw Android file-manager entries.

Images, audio players, and video players should share the same overall Oralith visual language while remaining visually distinguishable.

## 13. MEDIA POSITIONING / TEXT FLOW

This requirement is important.

A media element may occupy:

- part of the available width
- most of the width
- effectively the full width

When a media object uses most or all of the available width, surrounding text must not overlap it.

Text must maintain sensible spacing above and below the media.

When a media object is narrower and the editor design supports side placement, text may flow beside it.

Do not fake this using arbitrary hardcoded coordinates that only work on one screen size.

Build a layout model that can be recalculated correctly for different device widths and font scales.

When the user resizes media, the document layout should update correctly.

Media movement and resizing should feel direct and fluid.

Use the supplied Apple-design/animation principles:

- direct manipulation
- 1:1 tracking
- interruptibility
- appropriate spring behavior
- sensible boundaries
- velocity handoff where applicable
- accessibility/reduced-motion handling

Do not make gesture-driven interactions depend on rigid fixed-duration animations.

## 14. EDITOR TOOL SYSTEM

At the bottom of the editor, provide a horizontally scrollable tool area.

This tool area should contain actions such as:

- add image
- add video
- add audio
- add link
- formatting
- font
- text size
- text color
- bullet/list formatting
- select all
- other useful editor actions

The toolbar must remain usable on small screens.

Do not make every action permanently visible if that produces clutter.

Use secondary panels, sheets, popovers, or contextual tool rows when appropriate.

These panels should follow the supplied interaction and animation guidance.

## 15. MEDIA IMPORT EXPERIENCE

Do not make the core media-import experience look like a raw, generic file explorer.

The application should provide an Oralith-designed in-app media browser for local media where Android APIs allow it.

For example, it can present:

- images
- videos
- audio
- categories
- recent media
- file information

using a consistent Oralith interface.

Query Android's local MediaStore/library where appropriate.

When direct access to a file outside the indexed media library genuinely requires a system picker, isolate that system behavior behind the Oralith-designed flow rather than rebuilding dangerous storage behavior unnecessarily.

Do not request broad storage permissions when modern Android APIs provide safer alternatives.

## 16. AUDIO

Provide an audio block/player inside notes.

It should display meaningful metadata where available and provide simple playback controls.

Use an appropriate Android media playback library/API.

At minimum, design the architecture to handle common local formats such as:

- MP3
- AAC/M4A
- FLAC
- WAV
- OGG
- Opus

Do not claim universal format support unless Android/media capabilities actually support the format.

Where decoding support differs by Android version/device, handle failure gracefully and explain the problem to the user.

## 17. VIDEO

Provide a video block/player.

The player should be lightweight and should not automatically decode/play every video simultaneously in a long scrolling note.

Use efficient lifecycle-aware playback.

Support common formats that the chosen playback stack reliably supports.

Gracefully handle unsupported media.

## 18. IMAGES

Images should:

- load asynchronously
- be memory-conscious
- use appropriate sizing/downsampling
- avoid unnecessary full-resolution decoding
- preserve aspect ratio by default
- allow resizing in the editor

Use a reliable image-loading solution when justified, but keep the dependency footprint reasonable.

## 19. LINKS

Links can be inserted in two ways.

A. Insert a new link:

Show a polished dialog/sheet containing:

- Link title/display text
- URL

The visible text should be the title/display text.

The raw URL should not be the visual text by default.

B. Convert selected text into a link:

If the user selects text and chooses Insert Link, use the selected text as the display text and ask only for the URL where appropriate.

Links should have a clear visual distinction, including an underline by default.

They should remain readable and accessible.

## 20. TEXT FORMATTING

When text is selected, provide contextual formatting actions.

Support at minimum:

- bold
- italic
- underline
- text size
- text color
- font
- bullets/list formatting
- link

Add other formatting only when it provides real value and does not clutter the interface.

Formatting applies to selected text only.

Selecting all must select document text/content where appropriate, but operations such as changing font size must NOT resize:

- images
- audio
- video
- other media blocks

The editor must keep text formatting logically separate from media dimensions.

## 21. FONT SYSTEM

Allow users to change fonts for selected text.

Use bundled, license-compatible free fonts.

Prefer high-quality, widely used fonts from sources such as Google Fonts when their licensing permits bundling.

Do not download fonts dynamically every time the application runs.

Do not bundle dozens of fonts just for marketing value.

Select a sensible curated set of useful fonts for documents and multilingual text.

The font architecture must allow more fonts to be added later without rewriting the editor.

## 22. TEXT SIZE

Provide an editor text-size control.

The user should be able to:

- increase text size
- decrease text size
- apply size to the selected text
- select all text and change size

Do not let the text-size control accidentally resize media.

Respect accessibility/dynamic text sizing where technically appropriate.

## 23. BULLETS / LISTS

Provide a tool for creating bullet/list items at the cursor position.

Support multiple bullet/list styles where practical, for example:

- filled bullet
- hollow bullet
- numbered list

Do not implement a visually complicated system unless the underlying document model can support it cleanly.

## 24. TOOLBAR / SECONDARY CONTROL LAYERS

The editor may expose multiple layers of tools.

For example:

Primary horizontal tool row
→ user selects Formatting
→ secondary horizontal formatting controls appear
→ another control row may expose parameters such as:

- size
- color
- font

These layers should not feel like stacked dialogs.

They should feel like one spatially coherent tool system.

Use sheets/popovers/contextual bars when they communicate hierarchy better.

Keep interaction fast.

Do not force users through unnecessary confirmation steps.

## 25. UNDO / REDO

Undo and redo must operate on meaningful document edits.

Do not implement fake buttons that merely change visual state.

The editor architecture should have a proper command/history approach appropriate for text, formatting, media insertion, movement, resizing, and deletion.

Avoid retaining enormous unbounded histories in memory.

## 26. TOP EDITOR BAR

The note editor top area should contain:

- back/navigation control
- note title/context
- undo
- redo
- export/share-related action

Use appropriate spacing and hierarchy.

Do not crowd the top bar.

When content is being edited, preserve access to undo/redo without making the interface visually noisy.

## 27. SAVE MODEL

The user specifically wants saving to be highly efficient.

Use Room for structured note persistence.

Suggested architecture:

UI
→ ViewModel/state holder
→ repository
→ Room DAO

Media:

editor
→ application-managed media storage
→ Room metadata/reference

Do not block the UI during saves.

Do not write a full large document to disk on every keystroke.

Use incremental/debounced persistence and clear lifecycle handling.

Ensure a note is not silently lost when:

- navigating away
- rotating/configuration changes
- backgrounding the app
- process death
- application restart

## 28. EXPORT SYSTEM

The editor must provide export options including at minimum:

- DOCX
- plain text
- PDF

Exports should happen off the main thread.

Do not freeze the editor while generating an export.

Show progress when an export is non-trivial.

Handle export failures gracefully.

## 29. EXPORT COMPATIBILITY CHECKING

Before exporting, analyze the document for content that the selected format cannot safely represent.

For example, if a particular export implementation cannot represent:

- an embedded media type
- an unsupported video
- a certain font
- an unsupported formatting structure
- another document element

do NOT silently discard the content.

Instead:

1. explain clearly why the export cannot be completed
2. identify the incompatible content
3. visually highlight the offending content inside the editor
4. explain what the user can change
5. let the user dismiss the warning

The user specifically wants the problematic content highlighted in the note.

The highlight/error treatment should be clear but not destructive.

Tapping elsewhere should dismiss the visible error emphasis where appropriate.

A double tap may also clear the temporary error highlighting as part of the requested interaction.

Do not delete or modify the user's content when highlighting an export problem.

## 30. EXPORT ARCHITECTURE

Create an export abstraction rather than putting all export logic inside the editor UI.

Conceptually:

`ExportService`

with format-specific implementations such as:

- `DocxExporter`
- `PdfExporter`
- `TextExporter`

Do not force every format through one fragile giant function.

Choose lightweight, well-supported approaches.

For formats where library support is insufficient, implement only what is technically reliable instead of pretending to support everything.

## 31. ACCESSIBILITY

Accessibility is a first-class requirement.

Provide:

- content descriptions where needed
- adequate touch targets
- readable contrast
- semantic labels
- keyboard/text-input compatibility
- sensible dynamic text scaling
- reduced-motion handling
- appropriate focus behavior

Do not let sophisticated animations break usability.

## 32. ANIMATION RULE

Animation is part of interaction design, not decoration.

Follow all animation-related skills in the repository.

Prioritize:

- instant interaction feedback
- smooth gesture tracking
- interruptibility
- spatial consistency
- appropriate spring behavior
- subtle materialization
- meaningful state transitions
- reduced-motion support

Do not animate everything.

Avoid excessive bounce.

Do not introduce animation delays just to look fancy.

Never sacrifice interaction responsiveness for animation.

## 33. RESPONSIVE DESIGN

The application must behave correctly across:

- small Android phones
- large phones
- tablets
- portrait
- landscape
- different font scales
- different screen densities

Do not hardcode coordinates that only work on one device.

Use adaptive layout techniques.

Media resizing and text flow must remain correct when available width changes.

## 34. QUALITY OF CODE

The code should be production-oriented.

Requirements:

- clear naming
- small focused functions
- state hoisting
- immutable UI models where appropriate
- minimal unnecessary recomposition
- lifecycle awareness
- coroutine best practices
- structured concurrency
- no memory leaks
- no blocking calls on the main thread
- no duplicated business logic
- no giant god classes
- no giant god composables
- no unexplained magic numbers
- reusable design-system components

Keep the project easy to extend when Clock and Calculator are added later.

## 35. TESTING

Add meaningful tests for the architecture you create.

At minimum, cover important logic such as:

- note persistence
- document serialization/deserialization
- undo/redo behavior
- link creation
- formatting state
- media metadata handling
- export compatibility validation

Add Compose/UI tests for critical flows where practical.

Do not write meaningless tests merely to increase coverage numbers.

## 36. BUILD VERIFICATION

After implementation:

- run Gradle checks
- compile the application
- run relevant tests
- fix warnings/errors that are directly introduced by your changes
- verify the app launches
- verify navigation
- verify note creation
- verify editing
- verify persistence
- verify undo/redo
- verify media insertion architecture
- verify export validation
- verify empty Clock/Calculator/To-do placeholders

Do not consider the task finished merely because the code looks correct.

## 37. IMPORTANT SCOPE BOUNDARY

For THIS implementation phase, fully develop the Notes experience and its required architecture.

Do NOT fully implement:

- Clock
- Calculator
- To-do functionality

They should only have clean placeholders/scaffolding so they can be developed later without restructuring the entire project.

## 38. DEVELOPMENT PROCESS

Before writing code:

1. inspect the repository
2. read all files in `skills/`
3. inspect the existing Gradle/version setup
4. inspect the current theme
5. inspect the current activity
6. determine what can be reused
7. design the architecture
8. identify any dependency that is actually necessary
9. only then begin implementation

Do not immediately start replacing files before understanding the project.

## 39. DO NOT OVERENGINEER

The architecture must be scalable, but do not introduce unnecessary abstractions.

Do not create interfaces for everything.

Do not create ten classes where one focused class is enough.

Do not add networking because a local feature is inconvenient.

Do not add C++ because performance sounds important.

Do not add a third-party library when AndroidX/Compose can do the job cleanly.

Every dependency should have a reason.

## 40. FINAL UI REVIEW — MANDATORY

Before declaring completion, perform a design review using the repository's supplied skill files.

Review:

- hierarchy
- spacing
- typography
- icon consistency
- touch targets
- visual density
- interaction feedback
- animation
- gesture behavior
- sheets/popovers
- toolbar behavior
- media cards
- text editing
- responsive behavior
- empty states
- dark/light treatment
- accessibility
- reduced motion
- performance

Then correct issues you find.

The result should look like a carefully designed premium application, not a default Android Studio project with features added on top.

## 41. MOST IMPORTANT FINAL PRINCIPLE

Do not interpret this prompt as permission to take shortcuts.

When a requirement is complex, solve the architectural problem properly rather than replacing it with a fake approximation.

When something is technically impossible or constrained by Android/platform/export limitations, implement the strongest technically correct behavior and communicate the limitation clearly in the application.

Never silently lose user data.

Never silently discard unsupported document content.

Never compromise local privacy.

Never sacrifice maintainability for speed of implementation.

The application should ultimately feel like one coherent product called:

`Oralith`

with a consistent design language throughout.