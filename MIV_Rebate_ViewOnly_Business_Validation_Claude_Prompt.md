# MIV View-Only vs Rebate App — Business Validation Presentation

## 1. Primary Objective

I am providing you with a document containing screenshots and information from the **Rebate App** and the corresponding **MIV App** screens.

The same document/presentation will be shared directly with business stakeholders.

The purpose of this review is to allow the business to **verify that the MIV App correctly represents the view-only version of the Rebate App**.

This is a **business validation and screen-parity exercise**, not a UI redesign presentation.

For every relevant screen, clearly show:

**Rebate App → Corresponding MIV App**

The business should be able to visually compare the two and determine whether the MIV representation is correct.

Accuracy and traceability are more important than decorative presentation.

---

## 2. Source of Truth

The provided document is the source material.

It contains screenshots and information describing:

- Rebate App screens
- MIV App screens
- Corresponding workflows
- Relevant fields/data
- Existing annotations or explanations

Do not invent information that is not present in the source document.

Do not assume that two screens are equivalent simply because they look similar.

Where correspondence is uncertain, clearly mark it as:

**Needs Business Confirmation**

rather than making an assumption.

---

## 3. Core Concept

The presentation should consistently communicate:

### REBATE APP
The original/reference application.

↓

### MIV APP
The view-only representation of the corresponding Rebate App experience.

The objective is to validate that:

- the correct information is displayed
- the correct fields are represented
- the values/data correspond
- the structure is appropriate
- the relevant sections are present
- the view-only behavior is appropriate
- no unintended editable functionality is introduced

---

## 4. Do Not Frame This as a Redesign

Do NOT describe differences as:

- "better UI"
- "improved design"
- "modernized experience"
- "enhanced UX"

unless explicitly stated in the source material.

A visual difference does not automatically mean an incorrect implementation.

The key question is:

> **Does MIV correctly represent the business-relevant information and view-only experience of Rebate App?**

Some UI differences may be intentional because MIV is a view-only representation.

---

## 5. Presentation Structure

### Slide 1 — Title

**MIV App — Rebate App View-Only Validation**

Subtitle:

**Business Review & Screen Parity Verification**

---

### Slide 2 — Purpose

Explain the purpose clearly:

> The objective of this review is to validate that the MIV App correctly represents the relevant information and user view available in the Rebate App, while providing a view-only experience.

Include three objectives:

1. Validate screen correspondence.
2. Validate displayed information/data.
3. Validate view-only behavior.

---

### Slide 3 — Validation Model

Create a simple visual:

```text
┌─────────────────────┐
│     REBATE APP      │
│  Reference View     │
└──────────┬──────────┘
           │
           │ Compare
           ▼
┌─────────────────────┐
│       MIV APP       │
│    View-Only View   │
└─────────────────────┘
           │
           ▼
     Business Review
           │
     ┌─────┴─────┐
     │           │
   Match      Question
     │           │
  Confirm    Investigate
```

---

## 6. Screen-by-Screen Validation

For every corresponding screen, create a dedicated comparison slide.

Use this layout:

### [Screen / Business Function]

#### REBATE APP
[Large screenshot]

#### MIV APP
[Large screenshot]

Then provide a concise validation summary.

**Validation Focus**

- Screen purpose
- Key information
- Fields
- Values
- Sections
- View-only behavior

---

## 7. Visual Comparison

When useful, use a side-by-side layout:

```text
┌──────────────────────┬──────────────────────┐
│      REBATE APP      │        MIV APP       │
│                      │                      │
│     SCREENSHOT       │      SCREENSHOT      │
│                      │                      │
└──────────────────────┴──────────────────────┘
```

Keep corresponding screens aligned as closely as possible.

The screenshots should be large enough for business users to inspect.

---

## 8. Callouts

Use matching numbered callouts on both screenshots.

Example:

```text
REBATE APP                         MIV APP

     ①                                ①
 [Field A]                         [Field A]

     ②                                ②
 [Field B]                         [Field B]

     ③                                ③
 [Value]                           [Value]
```

Then below:

### Validation

**① Field A**  
Present and represented in MIV.

**② Field B**  
Present and represented in MIV.

**③ Value**  
Displayed value corresponds to the Rebate App.

This makes the validation objective extremely clear.

---

## 9. Data / Field Validation

Where the screenshots allow meaningful comparison, identify important fields explicitly.

Use a table when useful:

| Validation Item | Rebate App | MIV App | Status |
|---|---|---|---|
| Field / Section | Present | Present | ✓ |
| Business Value | X | X | ✓ |
| Date | X | X | ✓ |
| Status | X | X | ✓ |
| Action | Editable | View Only | Expected |

Use **Match / Difference / Needs Confirmation** rather than inventing a pass/fail determination when the evidence is insufficient.

---

## 10. View-Only Validation

This is a critical part of the presentation.

Identify areas where Rebate App allows an action but MIV should only display the information.

Clearly distinguish:

### Reference App
What the user can see/do.

### MIV
What the user should see.

### Validation
Whether MIV correctly provides the required information without unintended editing capability.

Example:

```text
REBATE APP
View + Edit

        ↓

MIV
View Only
```

Do not interpret the removal of editing controls as a defect if the requirement is view-only.

---

## 11. Differences

Not every difference is an error.

Classify differences into three categories:

### EXPECTED DIFFERENCE

Difference is consistent with the view-only MIV requirement.

Examples:

- Edit button absent
- Update action absent
- Editable field becomes read-only

### REPRESENTATION DIFFERENCE

UI looks different, but the underlying business information appears equivalent.

Mark for business review if necessary.

### POTENTIAL DEFECT / MISMATCH

Important business information, field, value, section, or behavior appears missing or incorrect.

Do not label something a defect unless the source material provides enough evidence.

---

## 12. Validation Status

Use simple status indicators throughout the deck:

**MATCH**

The information appears correctly represented.

**EXPECTED VIEW-ONLY DIFFERENCE**

Difference is expected because MIV is view-only.

**NEEDS BUSINESS CONFIRMATION**

The screenshots alone are insufficient to determine correctness.

**POTENTIAL MISMATCH**

There appears to be a meaningful discrepancy requiring investigation.

Do not automatically mark every screen as "PASS."

---

## 13. Business Review Questions

Where appropriate, include a small section:

### Business Confirmation

1. Does the MIV screen represent the intended Rebate App information?
2. Are all required fields/sections present?
3. Are the displayed values correct?
4. Are differences from Rebate App expected because MIV is view-only?
5. Is any required information missing?
6. Is any information displayed incorrectly?

This allows the same presentation to function as the business review artifact.

---

## 14. Interactive Navigation

Make the presentation interactive.

Create an overview/index:

```text
MIV VALIDATION

[1] Overview
[2] User / Summary
[3] Rebate Details
[4] Financial Information
[5] History
[6] Additional Details
[7] Validation Summary
```

Each item should link to the relevant section.

Each detailed screen should have:

**← Back to Validation Index**

Where practical, make the Rebate App and MIV screenshots clickable to larger/zoomed comparison slides.

---

## 15. Progressive Comparison

For complicated screens, use multiple slides.

### Slide A
Full Rebate App + MIV comparison.

### Slide B
Zoom into Section 1.

### Slide C
Zoom into Section 2.

### Slide D
Zoom into Section 3.

### Slide E
Validation summary.

This allows business users to inspect details without making the main slide unreadable.

---

## 16. Preserve the Evidence

The screenshots are evidence for business validation.

Therefore:

- Preserve original screenshots.
- Do not crop out important context.
- Do not alter displayed values.
- Do not modify UI elements.
- Do not make screenshots look artificially identical.
- Do not hide differences.
- Do not annotate over important data.
- Use separate copies for annotations and zooms.

The original screenshots should remain available in the presentation or supporting materials.

---

## 17. Business-Facing Language

Avoid technical implementation terminology unless necessary.

Do not focus on:

- React
- APIs
- databases
- backend services
- architecture
- code
- infrastructure

Focus on:

- screen
- information
- field
- value
- user action
- view-only
- correspondence
- validation
- difference
- business confirmation

---

## 18. Speaker Notes

Add concise speaker notes explaining what the presenter should say.

For each comparison:

> "This slide compares the Rebate App reference screen with the corresponding MIV view. The purpose is to confirm that the required business information is represented correctly. The absence of edit actions is expected because MIV provides a view-only experience."

Do not read every field aloud.

Focus the presenter on the important validation points.

---

## 19. Final Business Message

The presentation should ultimately communicate:

> **MIV is intended to provide a view-only representation of the relevant Rebate App experience. This review allows the business to validate that the corresponding information, fields, values, and screens are correctly represented, while differences caused by the view-only requirement are intentionally distinguished from potential mismatches.**

---

## 20. Quality Control

Before delivering the final PowerPoint, verify:

### Screenshot accuracy

- Correct Rebate App screenshot
- Correct MIV screenshot
- Correct screen pairing
- No accidental screenshot substitution

### Comparison accuracy

- Corresponding areas are correctly identified
- Values have not been misread
- Differences are not overstated
- Expected view-only differences are clearly distinguished

### Presentation quality

- Screenshots are readable
- Callouts are aligned
- Text is readable when projected
- No overlapping objects
- No clipped screenshots
- No broken images

### Navigation

- Overview links work
- Back buttons work
- Detail/zoom navigation works
- All hyperlinks point to the correct slide

---

## 21. Final Deliverable

Create:

**[Project_Name]_MIV_Rebate_ViewOnly_Business_Validation.pptx**

Optionally create:

**[Project_Name]_MIV_Rebate_ViewOnly_Business_Validation.pdf**

The PowerPoint is the primary deliverable.

The final presentation must be ready to send directly to the business for review.

---

# Final Instruction

Do not turn this into a generic product presentation.

This is a **business validation artifact**.

The central question on every comparison is:

> **"Does MIV correctly represent the corresponding Rebate App experience as a view-only application?"**

Build the presentation so that a business stakeholder can answer that question **screen by screen, field by field, and workflow by workflow**.
