Refactor the existing application to follow the design system described below.

Implement the changes in the application. Preserve its existing functionality, routes, data, forms, validation, and integrations. Inspect the current components before editing, then apply this design language consistently across all relevant screens.

The visual reference is “しるす”: a Japanese workplace application that feels calm, personal, organized, and quietly polished.

Treat this as a complete design system, not a change to the primary color and border radius.


DESIGN INTENT

The application should feel like a thoughtfully designed personal work journal.

Its personality is:
- Calm and reassuring.
- Softly rounded.
- Precise enough for daily professional use.
- Human without becoming playful or childish.
- Spacious without wasting the user’s time.
- Japanese in its typography, language, and attention to small details.

The central visual relationship is a deep, solid-colored navigation area beside a very light workspace. White surfaces, pale theme-colored panels, and dark, readable text create the hierarchy.

Spend the strongest visual emphasis on the user’s main task. Everything else should help the user understand and complete that task.

For attendance management, the main task is recording the working day. The clock, workplace selector, and clock-in button should have more prominence than monthly statistics.

Avoid turning the interface into a grid of equally important metric cards.


PRESERVE THE EXISTING PRODUCT

Keep:
- Existing business logic and backend connections.
- Existing user data and state.
- Routes, permissions, and authentication behavior.
- Existing validation and error handling.
- Features that users already rely on.
- Meaningful information density.

Refactor the presentation and interaction styling without replacing functioning features with static placeholders.

If the existing product serves a different purpose from attendance management, preserve that purpose. Translate the visual principles to its real workflows.

Do not introduce a demo-only design comparison bar or a selector for unrelated app designs.


COLOR SYSTEM

Use semantic color tokens throughout the application.

The default palette is:

--accent:        #174B42
--ink:           #1E3536
--muted:         #5A696C
--page:          #F8FAF9
--surface:       #FFFFFF
--line:          #DFE6E5
--soft:          #EFF2F2
--tint:          #E1E8E6
--tint-strong:   #BECDCA
--sidebar-text:  #D8E0DF
--sidebar-muted: #B2C4C1

Assign these colors specific jobs:

accent:
The main brand color. Use for the desktop sidebar, primary buttons, important icons, selected controls, and clock hands.

ink:
Primary text, headings, important values, and table contents.

muted:
Supporting descriptions, secondary labels, metadata, and inactive supporting icons.

page:
The main application background. It should look almost white, with a subtle relationship to the selected theme.

surface:
White panels, dialogs, form surfaces, and inactive calendar cells.

line:
Quiet one-pixel borders and separators.

soft:
Large supporting surfaces, such as the daily timeline, contextual notices, and theme preview panel.

tint:
Selected navigation items, the current day, and other selected backgrounds.

tint-strong:
Selected borders, timeline connections, and small supporting details.

sidebar-text:
Primary text and icons on the dark sidebar.

sidebar-muted:
Secondary organization information and supporting sidebar copy.

The page should remain predominantly light. Strong color should be concentrated in navigation and meaningful actions.

Avoid decorative gradients, glowing outlines, large translucent color blobs, and unrelated accent colors.

Do not use pure black for the main text. Use the theme-related ink token.


CUSTOMIZABLE THEMES

Provide a theme-color feature with six presets:

深緑: #174B42
海青: #286579
藍:   #424E8A
藤:   #77558D
木苺: #964B64
琥珀: #846127

Also allow the user to select a custom color.

Changing the theme must update the full visual system:
- Desktop sidebar.
- Primary buttons.
- Selected navigation.
- Clock accents.
- Selected calendar day.
- Tinted supporting surfaces.
- Borders and separators.
- Relevant icons.
- Theme preview.
- Focus indicators.

Keep white surfaces white.

Use a coordinated palette derived from one accent instead of manually assigning unrelated shades to individual components.

For palette generation, define:

mix(A, B, t) = A × (1 − t) + B × t

Mix each RGB channel and round to the nearest integer.

Using the effective accent color:

ink           = mix(accent, #222A31, 0.68)
muted         = mix(accent, #6B7076, 0.80)
page          = mix(accent, #FFFFFF, 0.97)
line          = mix(accent, #FFFFFF, 0.86)
soft          = mix(accent, #FFFFFF, 0.93)
tint          = mix(accent, #FFFFFF, 0.87)
tint-strong   = mix(accent, #FFFFFF, 0.72)
sidebar-text  = mix(accent, #FFFFFF, 0.83)
sidebar-muted = mix(accent, #FFFFFF, 0.67)

Before generating the palette, check whether white text remains readable on the accent.

If white text contrast is below 4.8:1, progressively darken the effective accent by mixing it toward #111820. An 8% mix per iteration works well. Recheck the contrast after each iteration.

Preserve the user’s original selected color separately from the adjusted effective accent.

Changing the theme should not recolor semantic warnings, errors, or success states indiscriminately. Their meaning must remain recognizable.

Persist the selected color in localStorage or the application’s existing preference system. Restore it when the application opens. Validate saved values and fall back gracefully to the default.

Apply preferences without discarding attendance data or other application state.

If saving the preference fails, allow the current visual change to work and explain that it could not be saved.


TYPOGRAPHY

Use these font families deliberately:

Japanese interface:
"Zen Kaku Gothic New", sans-serif

Clocks and prominent numerical information:
"Manrope", "Zen Kaku Gothic New", sans-serif

Use the Japanese Gothic family for:
- Navigation.
- Headings.
- Buttons.
- Form labels.
- Explanatory text.
- Japanese table content.

Use Manrope selectively for:
- Digital clocks.
- Calendar dates.
- Time values.
- Numerical summaries where it improves clarity.

Do not apply a monospace font to ordinary labels or metadata.

Recommended hierarchy:

Page greeting:
28–32px desktop.
22–25px mobile.
Weight 700.
Line height 1.5–1.65.

Section heading:
17–20px.
Weight 700.
Line height around 1.5.

Panel heading:
14–16px.
Weight 700.

Body:
14–15px.
Weight 400 or 500.
Line height 1.65–1.8.

Buttons and form labels:
13–14px.
Weight 500 or 700 depending on importance.

Secondary labels:
12–13px.
Weight 400 or 500.

Nonessential metadata:
11–12px, used sparingly.

Main digital clock:
Approximately 52–64px desktop.
Approximately 42–48px in compact mobile layouts.
Weight 500.
Line height around 1.15.
Tabular numerals.

Seconds:
Approximately 16–20px.
Muted color.
Aligned near the baseline of the main time.

Use a restrained type scale. Do not make every label bold.

Keep Japanese tracking subtle:
- Headings: approximately 0.02–0.04em.
- Body: normal or very slightly open.
- Numerals: tight and controlled.

Use font-variant-numeric: tabular-nums for changing time values so the layout does not move every second.

Keep normal text left-aligned. Center only elements that benefit from it, such as clock faces, status illustrations, and compact selection controls.

Handle Japanese line breaks intentionally. Avoid leaving a final character or punctuation mark isolated on a new line. On mobile, break a greeting into meaningful phrases.

Do not emphasize isolated words with unrelated colors, italics, or oversized typography.


SHAPE SYSTEM

Roundness is a defining part of this interface.

Use a hierarchy of radii rather than assigning one radius to every component:

Large primary panels:       26px
Contextual notice panels:   26px
Dialogs:                    28px
Standard cards:             20px
Weekly calendar cells:      18px
Large location options:     17px
Buttons and navigation:     15px
Inputs and compact fields:  12px
Toasts:                     18px
Status badges:              30px or fully pill-shaped
Avatars and swatches:       Circular

Mobile adjustments:

Large panels:               22px
Dialogs:                    25px
Standard cards:             19px
Weekly calendar cells:      14px
Buttons:                    14px

The result should feel soft and composed.

Do not make every rectangular element a pill. Pill shapes belong primarily to statuses, small theme controls, and compact filters.

When two sections share one outer panel, apply the large radius to the outer container. Internal divisions should meet cleanly without introducing unnecessary rounded gaps.

Nested corners should feel consistent. Smaller inset elements should have smaller radii than their parent.


SPACING AND DENSITY

Use a consistent spacing vocabulary:

4, 8, 12, 16, 20, 24, 32, 40, 48px

Typical values:
- Icon to label: 8–12px.
- Related text lines: 4–8px.
- Related controls: 8–12px.
- Standard panel padding: 24–28px.
- Mobile panel padding: 20–22px.
- Major section separation: 28–36px.
- Desktop workspace gutters: 32–48px.
- Mobile page gutters: 16–20px.

Use whitespace to explain relationships.

A heading should sit closer to the content it introduces than to the section above it.

Leave breathing room around the main action. Keep operational lists and tables efficient enough to scan.

Do not add large empty areas simply to make the interface look “premium.”


APPLICATION SHELL

Desktop:

Use a persistent left sidebar approximately 220–230px wide.

The sidebar contains:
- A compact brand mark and Japanese wordmark.
- Organization or workspace information.
- Main navigation.
- A small amount of quiet supporting content when useful.
- Help and the user profile near the bottom.

Use a solid accent background.

Navigation:
- Simple outline icon on the left.
- Japanese label.
- Approximately 48px row height.
- Generous horizontal padding.
- 15px rounded corners.
- Muted light text for inactive items.
- A pale tint background and dark accent text for the selected item.

The active state must remain obvious without relying only on icon color.

Main workspace:

Place a quiet header above the content:
- Current section or breadcrumb on the left.
- Theme control, date, and notifications on the right.
- A subtle bottom separator.
- Approximately 72px height.

Keep the content aligned to a consistent left edge. Constrain very wide layouts to a sensible maximum content width, around 1400px.

Compact desktop or tablet:

Collapse the sidebar to an icon rail around 72–80px wide when needed.

Retain accessible labels and tooltips for icon-only navigation.

Mobile:

Replace the persistent sidebar with a compact top header:
- Brand on the left.
- Theme palette button.
- Menu button.

Expose navigation through a controlled menu or drawer.

Do not squeeze full desktop navigation labels into a narrow column.


PAGE COMPOSITION

For the attendance home screen, use this hierarchy:

1. A personal greeting and date.
2. The main attendance action area.
3. This week’s attendance.
4. Recent attendance records.
5. A contextual notice.

The greeting should be brief:
“山田さん、今日も、よい一日を。”

Supporting text can be:
“一日のはじまりを、ここにしるす。”

Keep the greeting modest in scale. It is part of a working application, not a marketing hero.

The main action area should be one composed panel with two related regions:

Left, approximately 60–65%:
- “今日の打刻”
- Current work status
- Analog clock
- Digital time
- Workplace selector
- Main attendance action

Right, approximately 35–40%:
- “今日のながれ”
- Today’s chronological activity
- Total working time

Use a white background for the action region and a soft tinted background for the timeline.

Separate them with a quiet one-pixel border.

Treat the outer container as a single large rounded shape.


CLOCK TREATMENT

The clock is a distinctive, useful visual.

Use a clean analog wall-clock motif:
- Circular pale background.
- Subtle white inset rim.
- Fine minute marks.
- Slightly stronger hour marks.
- Small numerals at 12, 3, 6, and 9.
- Dark accent-colored hands.
- Minimal center pin.
- An optional restrained warm-colored second hand.

Avoid:
- Photorealistic textures.
- Metallic effects.
- Heavy shadows.
- Glossy surfaces.
- Elaborate illustrations around the clock.

The digital clock provides the precise time. The analog clock adds recognition and character.

They should show the same time.

Do not let continuous clock updates create unnecessary screen-reader announcements or layout changes.


BUTTONS AND ACTION HIERARCHY

Primary action:
- Solid accent background.
- White text.
- Approximately 50–52px high.
- 15px radius on desktop.
- Clear action verb.
- Optional small leading icon.
- Strong enough to find immediately.

Examples:
“出勤する”
“退勤する”
“仕事に戻る”

Secondary action:
- White or very light background.
- Thin theme-related border.
- Dark text.
- Same general shape as the primary action.
- Lower visual emphasis.

Example:
“休憩する”

Text action:
- Compact.
- Dark or accent-colored text.
- Optional small contextual icon.
- No decorative trailing arrow on every link.

Keep the main action predictable as the user moves through states.

Use descriptive disabled states. Do not allow the visual design to imply that an unavailable operation can be performed.


WORKPLACE SELECTOR

Present the current workplace as a clear, compact control:
- Small outline location or building icon.
- Workplace name.
- Chevron indicating selection.
- Pale page-colored background.
- Approximately 12px radius.

Examples:
“表参道オフィス”
“自宅”
“外出先”

The selection dialog should show large, easy-to-compare options:
- Icon inside a soft rounded square.
- Workplace title.
- Brief supporting description.
- Checkmark on the selected option.
- Accent border and soft fill for the selection.

Do not use a map unless actual geographic information is necessary for the workflow.


DAILY TIMELINE

Use a simple chronological structure:
- A fine vertical connector.
- Small circular markers.
- Time values in a consistent column.
- Short activity names.
- Optional workplace or supporting text.

The current or most recent event should have the strongest marker.

Planned events should be quieter than completed records. Distinguish them with text, not color alone.

Use natural descriptions:
“一日のはじまり”
“お昼休憩”
“退勤予定”

Finish the timeline with a small total-hours row separated by a light rule.

Avoid oversized timeline icons, repeated cards for each event, or unnecessary numbering.


WEEKLY CALENDAR

Show seven compact day cells on desktop.

Each cell contains:
- Weekday.
- Day number.
- Workplace or schedule.
- Time range when space allows.

Use white cells with thin borders and 18px corners.

The current day uses:
- A tinted background.
- A stronger theme-related border.
- A small “今日” pill where it fits.

Weekend cells should recede gently while remaining readable.

On mobile:
- Preserve the seven-day rhythm if labels still fit.
- Simplify secondary details.
- Keep essential date and status information.
- Use 14px corners.
- Do not solve overflow by shrinking important text excessively.


TABLES AND RECORDS

Tables should feel quiet and precise.

Use:
- Left-aligned Japanese labels.
- Consistent alignment for time values.
- Tabular numerals.
- Subtle horizontal separators.
- Muted column headings.
- Comfortable but efficient row heights.

Avoid:
- Heavy outer grids.
- Vertical borders around every cell.
- Strong zebra striping.
- Colored containers around every value.
- Excessive badges.

Use small icons and restrained text to indicate workplace.

Rows may have a subtle hover fill and a clear detail action.

On smaller screens, prioritize essential columns. If necessary, use a contained horizontal scroll region or a deliberate compact row layout. Never allow the entire page to overflow horizontally.


CONTEXTUAL NOTICES

Use a softly tinted panel with a 26px radius.

Content:
- Small source or category label.
- Short, useful heading.
- One or two brief supporting sentences.
- A specific action when appropriate.

Example:
“今月の勤怠、月末までに確認を。”

A single small botanical outline can appear in a corner, using a pale theme-related color. Keep it subordinate to the content.

Do not turn notices into promotional banners.


THEME PICKER

Desktop entry:
A compact pill in the header containing:
- Palette icon.
- “テーマカラー”
- Small circular swatch of the current effective accent.

Mobile entry:
A compact palette icon and color indicator.

Dialog:
- Approximately 440–480px maximum width.
- 28px radius on desktop.
- 25px radius on mobile.
- White background.
- Comfortable padding.
- Restrained darkened backdrop.
- Clear heading and close control.

Heading:
“しるすのテーマカラー”

Description:
“サイドバーやボタンを、お好きな色に。”

Include:
- A small live preview showing the sidebar, primary action, clock, and calendar.
- Six circular preset swatches.
- Japanese preset names.
- Visible checkmark and selected styling.
- A custom color input.
- The selected hex value.
- A short note explaining automatic saving.
- “標準の深緑に戻す”
- “完了”

Color changes apply immediately. The “完了” button closes the dialog.

Use six swatches in one row when there is room. On very narrow screens, switch to a three-column layout.

Keep preset controls keyboard-accessible and expose their selected state programmatically.


FORMS AND DIALOGS

Inputs:
- White surface.
- One-pixel theme-related border.
- 12px corners.
- At least 44px comfortable control height.
- Clear labels above the input.
- Visible focus state.
- Helpful validation placed near the relevant field.

Do not rely on placeholder text as the field’s only label.

Dialogs:
- One clear title.
- Consistent padding.
- Clear primary and secondary actions.
- Logical keyboard focus.
- Focus restoration when closed.
- Accessible name.
- Escape-to-close behavior where appropriate.

Use color and text together for errors.

A failure should explain:
- What could not be completed.
- Whether the user’s changes remain.
- What the user can do next.


ICONS AND SMALL GRAPHICS

Use one consistent outline icon family, such as Lucide.

Typical sizes:
- Navigation: 20px.
- Buttons: 17–20px.
- Supporting metadata: 14–16px.

Use approximately 1.5–2px stroke weight.

Icons should support recognition. Avoid placing a decorative icon beside every sentence.

Simple circular avatars with initials or Japanese characters are acceptable.

Any custom illustration should use flat, restrained shapes and the same theme palette.

A small flower or leaf can provide a human detail. Use it sparingly; it should never compete with the main task.


BORDERS AND ELEVATION

Use borders and surface color as the primary methods of grouping information.

Borders:
- Usually 1px.
- Low contrast.
- Related to the selected theme.

Shadows:
- Nearly absent from ordinary content panels.
- Very subtle on the main panel if needed.
- Stronger only for actual overlays, dialogs, or floating feedback.

An example of a suitably quiet panel shadow:
0 4px 18px rgba(28, 50, 36, 0.012)

Avoid placing the same visible shadow beneath every card.

The overall interface should feel like an organized surface, with elevation reserved for elements that genuinely sit above it.


INTERACTION AND MOTION

Use restrained transitions around 120–180ms for:
- Hover fills.
- Border changes.
- Selection feedback.
- Control states.

Avoid:
- Card lifting on every hover.
- Decorative bouncing.
- Staggered entrances throughout the page.
- Continuous floating animations.
- Large animated color washes.

Motion should help explain a user-triggered change.

Respect prefers-reduced-motion.

Do not animate layout properties during theme changes. Avoid applying a universal transition to every element.


JAPANESE COPY

Use clear, natural Japanese throughout the product.

Prefer specific actions:
“出勤する”
“退勤する”
“休憩する”
“仕事に戻る”
“勤務記録を見る”
“申請を保存する”

Keep vocabulary consistent:
- 勤務場所
- 勤務記録
- 今日の打刻
- 今日のながれ
- 今週の勤務
- テーマカラー

The tone should be considerate and professional.

Use warmth in greetings and completion messages:
“今日も、よい一日を。”
“おつかれさまでした。”

Keep operational controls direct.

Avoid:
- Marketing claims inside routine workflows.
- Unnecessary English labels.
- Long technical explanations.
- Vague buttons such as “実行” when a specific verb is possible.
- Repeated decorative subtitles.


RESPONSIVE BEHAVIOR

Design intentional layouts for:
- Large desktop.
- Compact desktop or tablet.
- Mobile.
- Narrow mobile around 320px.

Desktop:
Dark sidebar, spacious workspace, split main panel.

Tablet:
Compact navigation rail, reduced gutters, rebalanced panel widths.

Mobile:
Top header, accessible menu, stacked main sections, comfortable controls.

The main task must remain easy to find at every size.

When a row becomes cramped:
- Reflow it.
- Stack related controls.
- Remove nonessential metadata.
- Preserve readable text and usable targets.

Do not simply scale the desktop screen down.

Check Japanese headings for awkward line breaks at each breakpoint.

Avoid content hidden beneath fixed controls. Account for mobile safe areas when necessary.


ACCESSIBILITY

Use semantic HTML and appropriate interactive elements.

Provide:
- Visible keyboard focus.
- Accessible names for icon-only buttons.
- Programmatic selected states.
- Proper form labels.
- Dialog focus management.
- Sufficient text contrast.
- Status text in addition to color.
- Reduced-motion support.

Aim for at least 4.5:1 contrast for ordinary text. Use a 4.8:1 target for white text on generated accent colors to provide a margin.

Ensure touch controls have comfortable hit areas, generally around 44px or larger even if the visible icon is smaller.

Do not reduce critical information to tiny, low-contrast text.


IMPLEMENTATION APPROACH

Start by auditing:
- Existing layout components.
- Shared buttons and form controls.
- Typography.
- Hard-coded colors.
- Border radii.
- Spacing.
- Responsive behavior.

Create or consolidate semantic tokens.

Apply the system in this order:
1. Application shell and page backgrounds.
2. Typography and content hierarchy.
3. Main task area.
4. Shared controls.
5. Lists, tables, and calendars.
6. Dialogs and notifications.
7. Theme preferences.
8. Responsive and accessibility refinements.

Use the project’s existing styling approach where practical.

Avoid piling conflicting overrides onto old styles. Consolidate outdated rules and keep selector specificity predictable.

Centralize theme generation and preference persistence.

Keep component styling scoped so this visual system does not accidentally recolor unrelated interfaces.


FINAL REVIEW

Before completing the refactor, verify:

- The sidebar and main action establish a clear hierarchy.
- The workspace remains light and calm.
- Large surfaces have visibly soft corners.
- Corners vary appropriately between panels, cards, and controls.
- Typography feels consistent and Japanese-first.
- The main task is more prominent than supporting statistics.
- Theme changes update all related surfaces coherently.
- Custom light colors still produce readable controls.
- Theme selection survives a reload.
- Resetting the theme works.
- Semantic status colors remain meaningful.
- Existing functionality still works.
- Dialogs and controls work with the keyboard.
- Desktop and mobile layouts have been visually inspected.
- There is no unintended page-level horizontal overflow.
- There are no awkward single-character Japanese line breaks.
- Decorative elements remain subordinate to useful content.

Deliver the implemented refactor and a brief explanation of what changed and how it was verified.

The finished application should feel like a calm Japanese work journal: a deep-colored navigation anchor, an almost-white workspace, coordinated pale surfaces, clear Gothic typography, precise numerical information, softly rounded controls, and one obvious next action.
