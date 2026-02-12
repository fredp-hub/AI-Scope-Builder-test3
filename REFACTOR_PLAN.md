# Component Refactor Plan
## Deferred from Audit Wave 3 — Requires dedicated sprint

### Priority 1: AssessmentReportEditor.tsx (3,272 lines)
Split into:
- AssessmentReportEditor/ (folder)
  - index.tsx (orchestrator, state management)
  - DURAThresholdPanel.tsx
  - LineItemEditor.tsx
  - RoofDamageSection.tsx
  - ElevationDamageSection.tsx
  - InteriorDamageSection.tsx
  - PendingItemResolver.tsx

### Priority 2: ConversationalScope.tsx (3,178 lines)
Split into:
- ConversationalScope/ (folder)
  - index.tsx (orchestrator)
  - MessageThread.tsx
  - ScopeDisplay.tsx
  - NarrativeEditor.tsx
  - ActionButtons.tsx
  - DocumentPanel.tsx

### Priority 3: ExtractedDataDisplay.tsx (2,954 lines)
Split into:
- ExtractedDataDisplay/ (folder)
  - index.tsx (orchestrator)
  - RoofDataSection.tsx
  - ElevationDataSection.tsx
  - InteriorDataSection.tsx
  - AuxiliaryDataSection.tsx

### Priority 4-6: ScopeEditor, SideBySideViewer, AddItemModal
Similar decomposition patterns.

### Lib files over 1,000 lines:
- scopeworx-field-report-utils.ts (3,316 lines) — Split by section
- calculator.ts (2,431 lines) — Split by calculation type
- claude-extractor.ts (1,642 lines) — Split by document type
- codeMatcher.ts (1,338 lines) — Split by component type

### Estimated effort: 3-5 days dedicated refactor sprint
### Risk: High regression risk — requires comprehensive testing after each split
### Prerequisite: Full test coverage on critical paths before decomposition
