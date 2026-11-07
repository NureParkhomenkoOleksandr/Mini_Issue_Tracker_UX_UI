# Mini Issue Tracker — Figma Design Implementation Brief v1.0

## Purpose and sources

Create editable grayscale low-fidelity desktop wireframes for a small internal issue tracker. This deliverable is a design file, not a working application.

Authoritative inputs: SD_Spec §1/3/5/8; Input Pack v1.0; Decision Log v1.1 (APPROVED D-01–D-14); Screen Map v1.0; Screen Contracts v1.0. This file is self-contained: follow the rules below without needing to fetch those inputs. US/AC/BR identify specification requirements; D IDs identify approved design decisions. Human confirmation covered the proposed interface details and three key boundary cases; it was not a complete independent audit of all criteria.

Release scope: US-01–US-08 only. Actors: two Team Members (Member A, Member B) and one Team Lead (Lead). Everyone is a pre-defined team member; only authenticated users can use the real product. Assignee is a relationship to an issue, not a new global role. [BR-01; D-02/08]

## Design constraints

Use one working page, grayscale, clear labels, readable desktop layouts, editable Figma-native text and shapes, local reusable components with actual instances, meaningful layer names and Auto Layout where appropriate. Keep long titles and descriptions readable in details. Do not create a flat image or a code-based app. Place test-actor labels, source annotations and technical notes outside product frames. [D-01/14]

Build canonical surfaces plus compact state examples. Do not build sixteen complete detail pages for role × status combinations. The initial inventory is seven top-level frames; variants inside the reference frame do not become additional product pages. Future manual prototype wiring may require technical copies, which must be named as copies of their canonical frame. [D-14]

At this generation step, annotate navigation intent only. Do not implement backend, authentication, persistence, conditional permissions, filtering algorithms or API code. Real prototype connections will be added and checked manually later. [D-02/08]

## Canonical frames and controls

### S-01 — Authentication boundary

An annotation frame containing the application name and “Authentication required — mechanism TBD”. It is a conceptual boundary, not a login form. No password, email, SSO, registration, role switcher or real login action. The demonstration starts in an already authenticated S-02-A context. [BR-01; NFR-02; D-02/14]

### S-02-A — Issues / All

Show application name, All and Important tabs, Create Issue, and a list/table with exactly these required columns: ID, Title, Status, Priority, Assignee. Display all six baseline issues from the sample data below, including Closed issues. There are no row-selection checkboxes. [AC-02.1/02.2; AC-05.1/05.3; D-01]

Controls: C-01 All tab; C-02 Important tab; C-03 Create Issue button; C-04 Title link for an existing issue. Title opens details for that same issue ID; the prior tab becomes the navigation origin. [AC-02.3; D-07/09]

### S-02-B — Issues / Important

Use the same list structure and controls with Important active. This is a filtered state of the same dataset, not an independent collection. Apply exactly:

`priority in {High, Critical} AND status != Closed`

For the baseline sample, show ISS-001 and ISS-003 only. High + Resolved is included. Critical + Closed, Low, Normal and absent priority are excluded. Display an empty Important variant reading “No important issues” if nothing matches; include that compact example in REF-01 rather than adding a new product page. [AC-08.1–08.4; BR-09/09.1; D-11]

### S-02-C — Issues / Empty All

All is active, no issue rows, message “No issues yet”, and Create Issue remains available. Tabs remain present. This is an empty dataset fixture, not a failed load and not the result of deleting issues. [AC-02.5; D-11]

### M-01 — Create Issue modal

A modal frame intended as an overlay above the calling list state. It contains only two user inputs: C-05 Title, required; C-06 Description, required and multiline. Actions: C-07 Create and C-08 Cancel. Default inputs are empty. Show labels and required indicators clearly. Do not ask the user to enter ID, status, priority, assignee, author or created time. [AC-01.1–01.5; D-01]

Keep Create available in the prepared validation examples. Missing Title displays “Title is required” (source Gherkin example). Missing Description displays “Description is required” (approved UX wording). If both are empty, show both errors. Invalid input creates no issue. Cancel closes the overlay without creating an issue and restores its exact calling state. Successful Create closes the modal and opens the prepared new issue ISS-007 in S-03; preserve the calling tab as origin. [AC-01.2/01.3; D-10/12]

### S-03 — Issue Details

Show ID, full Title, full Description, current Status, Priority, Assignee, Author and Created at. Absence of assignee is displayed as Unassigned. Group the Assignee/Priority/Status controls together, without a decorative “Control Actions Area” heading. Do not unnecessarily duplicate editable and read-only versions of the same value. Current values must remain readable when controls are disabled. [AC-02.4; AC-05.1/05.2; D-11]

Canonical example: Lead viewing ISS-003 assigned to Member A. Assignment and priority selectors are available to Lead; status selector and its Apply are disabled because Lead is not this issue’s assignee. Initial Apply buttons for unchanged values are disabled until another permitted choice is staged. [AC-07.4; D-05/13]

Controls:
- C-09 Assignee single select, C-10 adjacent Apply. Options: Member A, Member B, Lead. Only Lead can assign/reassign one team member, including themselves. No unassign/reset operation is introduced. [US-03, AC points 1–4; D-04/05/06]
- C-11 Priority select, C-12 adjacent Apply. Only Lead may set/change it. Show absence as Not Set; selectable levels are Low, Normal, High, Critical only. Not Set is not a fifth level or a reset action. [BR-04/05/06; AC-04.1/04.2; D-03/05/06]
- C-13 Status select, C-14 adjacent Apply. Only the current assignee may change status, including for Lead. Offer only the permitted destinations listed below. Current status is visible but is not offered as a new transition. [BR-08/08.1; AC-07.2–07.5; D-05/06/13]
- C-15 Comment multiline input, C-16 Add Comment. Available to all authenticated users, including on Closed issues. [US-06]
- C-17 Return to Issues List. Return to the prior All/Important tab. [D-07/10]

Assignment, priority and status use selection → adjacent Apply. Apply is disabled unless the actor has the right and has selected a different permitted value. Success updates the visible value and remains on S-03. Changing assignee changes the current status-permission relationship; it never creates multiple assignees. [D-04/06/13]

Comments: saved entries contain text, author and creation date/time. Empty submission shows “Comment cannot be empty” and creates nothing. Save failure shows “Could not save comment”, creates no saved entry and preserves the draft. Success shows the saved entry and clears the input. Include ready, empty-validation, saved and save-failure examples in REF-01. [AC-06.1–06.5; D-12]

New-issue example: show ISS-007 with Open, Not Set, Unassigned, current creator and created date/time. These are prepared system-result values, not extra inputs. [AC-01.4/01.5; AC-07.1; D-04/08]

### REF-01 — Verification reference, outside the product UI

Create compact labeled component examples or matrices with the following annotation IDs:
- N-01: authentication boundary and simulation limits.
- N-02: all four permission contexts in the matrix below, plus Unassigned.
- N-03: all four current statuses and their permitted destinations; include In Progress explicitly and no next action for Closed.
- N-04: Important predicate and High + Resolved / Critical + Closed / Not Set examples; empty Important example.
- N-05: Create default, missing Title, missing Description, both missing, and new-issue result.
- N-06: comment ready, empty validation, saved success and save failure; saved entries include author/time, failure has no new saved entry.
- N-07: Not Set versus selectable priority; Apply/Return navigation notes; implementation tests outstanding.

Label the test actor, issue ID and current status for each context. These labels are review annotations, not product controls. No user-facing role switcher. Use compact examples instead of duplicating entire detail pages. [D-14]

## Permission matrix

All contexts assume authentication. Disabled controls remain visible. A user’s assignee relationship is per issue. [D-05]

| Action | Member non-assignee | Member assignee | Lead non-assignee | Lead assignee |
|---|---|---|---|---|
| View / create / comment | Yes | Yes | Yes | Yes |
| Assign / reassign | No | No | Yes | Yes |
| Set / change priority | No | No | Yes | Yes |
| Change status | No | Allowed transitions only | No | Allowed transitions only |

Sources: BR-02/06/08, US-02/03/06, AC-07.4; D-04. If no assignee exists, nobody may change status before assignment. Closed has no allowed next status even for its assignee. Closed does not automatically disable comments, assignment or priority management. [BR-08.1; US-06]

## Status transition matrix

Only the current assignee may perform an allowed transition. [BR-08.1; AC-07.4]

| From / To | Open | In Progress | Resolved | Closed |
|---|---|---|---|---|
| Open | Current, not an action | Allowed | Forbidden | Forbidden |
| In Progress | Forbidden | Current, not an action | Allowed | Forbidden |
| Resolved | Forbidden | Allowed | Current, not an action | Allowed |
| Closed | Forbidden | Forbidden | Forbidden | Current, not an action |

Unknown values are not selectable. The status selector and Apply are disabled if the actor lacks permission or there are no destinations. Do not infer that any valid status is a legal destination from every other status. [AC-07.5; D-13]

## Sample data

All data below are fictional fixed fixtures, not database records. Display Created at as the supplied text; no real-time clock or persistence is needed. Lead is the canonical demonstration actor. [D-08]

| ID | Title | Description | Status | Priority | Assignee | Author | Created at |
|---|---|---|---|---|---|---|---|
| ISS-001 | Login fails | The application shows an error after a valid login attempt. | Open | Critical | Member A | Member B | 2026-11-01 09:15 |
| ISS-002 | Form layout breaks | The description field overlaps the submit button on the form. | In Progress | Normal | Member B | Member A | 2026-11-02 10:20 |
| ISS-003 | Export produces empty file | Exporting the issue list produces a file containing no rows. | Resolved | High | Member A | Member B | 2026-11-03 14:30 |
| ISS-004 | Old crash report | The previously reported crash was fixed and the issue was closed. | Closed | Critical | Lead | Member A | 2026-11-04 11:00 |
| ISS-005 | Help text typo | The help text contains a spelling error. | Open | Low | Unassigned | Lead | 2026-11-05 12:10 |
| ISS-006 | Missing image | The help page does not display its example image. | Open | Not Set | Unassigned | Member B | 2026-11-06 15:40 |
| ISS-007 | New issue example | The settings panel does not open when its button is clicked. | Open | Not Set | Unassigned | Lead | 2026-11-07 15:00 |

Baseline All contains ISS-001–ISS-006, Important contains ISS-001 and ISS-003. ISS-007 is a separate prepared successful-Create fixture, not an existing baseline row. For the canonical Create demonstration, prepare Title and Description matching ISS-007 before its success state; the default modal is still empty. If an annotation demonstrates creation by Member A instead, its author must be Member A, without changing the canonical Lead fixture.

Canonical ISS-003 existing saved comment:
- text: “The export fix is ready for verification.”
- author: Member A
- created at: 2026-11-06 16:10

Comment ready draft for Lead: “I will check the exported file.”
- success fixture: retain the existing entry and append that text with author Lead, created at 2026-11-07 15:05; clear the draft.
- failure fixture: retain only the existing entry, show the save error and keep the draft.
- empty-validation fixture: retain only the existing entry, show the empty-comment error.

## Navigation intent and prototype limits

Use annotation arrows or notes for these routes. Do not claim they are wired or tested in this generation.
- T-02: an issue Title opens its matching S-03 and remembers the calling tab.
- T-03/T-04: All ↔ Important; empty All remains a state of the same list.
- T-05/T-06: Create opens M-01 from All/Important/Empty; Cancel restores that exact calling state and creates nothing.
- T-07/T-08: missing required fields remain in modal with validation.
- T-09: successful Create opens S-03 for the new ISS-007, not the canonical existing ISS-003.
- T-10: Return restores the origin tab and displays the dataset appropriate to its predicate. A newly created Not Set issue is in All, not Important. A Closed issue disappears from Important, but the tab itself remains Important.
- T-11/T-12/T-13: assignment/reassignment/priority Apply remain on S-03 with the updated value.
- T-14/T-15/T-16/T-17: Open → In Progress → Resolved, Resolved → In Progress, Resolved → Closed; only current assignee.
- T-18/T-19/T-20: comment success/empty/failure remain on S-03 with the corresponding saved-entry result.
- T-21–T-24: unauthorized or invalid operations have no successful transition or data change.

Later manual P1 minimum: wire tabs, ISS-003 details from both tabs, Create/Cancel from both tabs, new-issue success and origin-preserving Return; inspect Empty All Create/Cancel separately. Technical copies may be required for origin preservation. Apply, status and comment examples must exist visibly; treat them as V-only unless actual connections are added and tested. Static examples do not prove interactive validation, saving, filtering or authorization. [D-08/14; Screen Contracts §10]

## Exclusions

Do not add title/description editing after creation, deletion, attachments, AI recommendations, categories, dashboards, analytics, notifications, search, sorting, pagination, user administration, user-visible change history, extra issue metadata, multiple assignees, new roles, extra priorities/statuses/transitions, priority reset, invented authentication, row selection, bulk actions, branding, decorative imagery, page icon placeholders or empty squares that resemble controls. Do not create separate product pages for assignment, priority, status, comments or Important Issues. These are the boundaries of this approved design scope; deletion/history and release exclusions also follow BR-10/11 and SD_Spec §8.

## Acceptance checklist and completion report

Before finishing, inspect the generated design against this checklist:
- Seven canonical frames with exact IDs and meaningful editable layers; actual components/instances and suitable Auto Layout.
- List data include required fields; details include full metadata; Create has exactly two user-input fields.
- Current status remains readable; Lead non-assignee cannot change it; all four permission contexts and all four current statuses are represented.
- Only the four permitted status transitions; Closed has none.
- Important includes High + Resolved and excludes Critical + Closed and absent priority.
- Not Set represents absence and is not a selectable priority/reset.
- Required-field validation and all comment outcomes are visible; saved comments include author/time; save failure creates no saved entry.
- Navigation annotations preserve origin, distinguish existing ISS-003 from new ISS-007 and show prepared outcomes honestly.
- No extra product functions or misleading decorative controls; review notes remain outside the product UI.

In the same response, report the exact frames created, actual reusable components and instances, and any rules/states that were not represented or remain uncertain. Describe actual work, not intended work. Do not perform additional redesign after giving the report. Do not claim full compliance based only on your own response.

A static design cannot verify actual authentication, server permissions, automatic IDs/time, persistence, real filtering, response time < 1 second, HTTPS or backup/restore. Keep these implementation checks explicitly outstanding. No exports are requested from the Agent at this step.
