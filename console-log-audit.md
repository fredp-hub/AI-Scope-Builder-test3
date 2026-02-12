# Console.log Audit Report - Scopient Codebase

**Generated:** 2026-01-29
**Total Statements:** 531

---

## Summary

| Category | Count | Action |
|----------|-------|--------|
| DEBUG (Remove) | ~320 | Delete - temporary debugging, emoji markers, verbose step logging |
| KEEP (Convert) | ~85 | Convert to console.error/console.warn - security and error context |
| CONDITIONAL | ~126 | Wrap in `process.env.NODE_ENV === 'development'` check |

---

## Top 15 Files by Console.log Count

| File | Count | Primary Category |
|------|-------|-----------------|
| `components/ConversationalScope.tsx` | 144 | DEBUG - Heavy step-by-step debugging |
| `app/api/conversation/start/route.ts` | 76 | DEBUG - Verbose step logging |
| `lib/hover-vision.ts` | 30 | CONDITIONAL - Processing diagnostics |
| `app/api/generate-pdf/route.ts` | 25 | DEBUG - Step timing logs |
| `app/api/documents/[id]/process/route.ts` | 25 | CONDITIONAL - Processing flow |
| `app/api/documents/process-queue/route.ts` | 19 | CONDITIONAL - Queue processing |
| `app/api/conversation/message/route.ts` | 19 | DEBUG - Message debugging |
| `components/providers/AuthProvider.tsx` | 17 | CONDITIONAL - Auth flow tracing |
| `app/api/documents/bulk-upload/route.ts` | 15 | CONDITIONAL - Upload progress |
| `app/(dashboard)/claims/ClaimsPageContent.tsx` | 15 | DEBUG - Load cycle debugging |
| `components/AssessmentReportEditor.tsx` | 11 | DEBUG - Emoji-marked debugging |
| `components/MasterInventoryEditor.tsx` | 10 | DEBUG - Component debugging |
| `app/(dashboard)/claims/[id]/page.tsx` | 10 | DEBUG - Delete flow debugging |
| `lib/claude-extractor.ts` | 9 | CONDITIONAL - AI processing |
| `app/api/scopes/route.ts` | 9 | CONDITIONAL - Scope operations |

---

## Category: DEBUG (Can Remove) - ~320 statements

These should be removed before production. Characterized by:
- Emoji prefixes (🔴, 🔵, 🟢, 🟡, 🎯, 📋, 📄, 💾, 📝, 🖱️, 🚀)
- `[STEP N]` pattern for verbose flow tracing
- `[DEBUG]` prefix
- Inline IIFE debugging: `{(() => { console.log(...); return null; })()}`
- Temporary data dumps with `.substring()` limits

### High-Priority Removals

**components/ConversationalScope.tsx** (144 statements)
```
Line 328-330: 🔍 AssessmentSummaryDisplay debugging
Line 485-486: 🟡 transformAssessmentData INPUT logging
Line 869-953: 📜 [HISTORY] verbose history loading
Line 1015-1144: 🎯 [DRAFT PDF] step-by-step debugging (30+ lines)
Line 1156-1272: 💾 [SAVE] step-by-step logging
Line 1362-1516: 🔴/🟢/🔵 START flow debugging (50+ lines)
Line 1566-1701: 🔴/🔵 SEND message debugging
Line 1860-2097: 📄 [PDF] extremely verbose generation logs (50+ lines)
```

**app/api/conversation/start/route.ts** (76 statements)
```
Line 32-303: 🔍 [STEP N] pattern throughout entire function
Line 343-449: 🔄 transformStartResponse verbose logging
Line 458-567: 🔵 Data structure debugging
Line 662-731: ⚠️ FALLBACK handler logging
```

**components/AssessmentReportEditor.tsx** (11 statements)
```
Line 504-510: 🔴 reportData debugging block
Line 951: 🎯 DURA threshold logging
Line 1059-1117: 🤖 AI enhancement debugging
Line 1425: Inline IIFE console.log (anti-pattern)
```

**app/api/conversation/message/route.ts** (19 statements)
```
Line 177-184: 💬 Verbose request body logging
Line 206-274: 🎯/📦/🔵 Action and payload debugging
```

---

## Category: KEEP (Convert to console.error/warn) - ~85 statements

These provide security and error context but should use appropriate log levels.

### Security Checks (Convert to console.warn)
Pattern: `console.log('🔒 ...: No authenticated user')`

```
app/api/claims/[claimId]/status/route.ts:14
app/api/claims/[claimId]/sync-from-documents/route.ts:22
app/api/documents/bulk-upload/route.ts:80
app/api/documents/link/route.ts:13, 74
app/api/documents/process-queue/route.ts:15, 335
app/api/documents/[id]/correct/route.ts:15, 101
app/api/documents/[id]/process/route.ts:80
app/api/documents/[id]/route.ts:16, 49
app/api/documents/[id]/signed-url/route.ts:46
app/api/enhance-report/route.ts:123 (convert to info)
app/api/generate-assessment/route.ts:27, 263
app/api/pdf/refresh-url/route.ts:41
app/api/scopes/route.ts:12, 66, 138
app/api/scopes/[id]/route.ts:14
app/api/test-n8n/route.ts:10
```

### Error Context (Keep as console.error)
```
lib/auth/cookie-auth.ts:39-74 - Auth debugging (conditional)
lib/slack/client.ts:64 - No Slack connection
lib/slack/notifications.ts:98, 104 - Slack config missing
```

---

## Category: CONDITIONAL - ~126 statements

These are useful for development/debugging but should be wrapped:

```typescript
if (process.env.NODE_ENV === 'development') {
  console.log('...');
}
```

### Auth Flow Tracing
**components/providers/AuthProvider.tsx** (17 statements)
```
Line 50-77: [Auth] profile fetching
Line 86-204: [AUTH] session initialization
Line 251-261: [AUTH] token refresh
```

### Data Loading Tracing
**app/(dashboard)/claims/ClaimsPageContent.tsx** (15 statements)
```
Line 143-240: [Claims] load cycle tracing
```

**app/(dashboard)/page.tsx** (9 statements)
```
Line 98-153: [Dashboard] load tracing
```

**app/(dashboard)/analytics/page.tsx** (3 statements)
```
Line 111-341: [Analytics] load tracing
```

### Document Processing
**lib/claude-extractor.ts** (9 statements)
```
Line 1132-1528: Extraction progress logging
```

**lib/hover-vision.ts** (30 statements)
```
Line 329-738: Vision processing diagnostics
```

**lib/document-classifier.ts** (3 statements)
```
Line 23-37: Classification result logging
```

### API Operations
**app/api/documents/bulk-upload/route.ts** (15 statements)
```
Line 85-346: Upload progress tracking
```

**app/api/documents/[id]/process/route.ts** (25 statements)
```
Line 87-320: Document processing flow
```

---

## Recommended Actions

### Phase 1: Immediate Cleanup (High Impact)
1. **Remove all emoji-prefixed logs** - Search pattern: `console.log\(['"][\p{Emoji}]`
2. **Remove [STEP N] pattern logs** - Search: `console.log.*\[STEP`
3. **Remove inline IIFE debugging** - Search: `{(() => { console.log`
4. **Remove [DEBUG] logs** - Search: `console.log.*\[DEBUG\]`

### Phase 2: Convert Security Logs
Replace all `console.log('🔒` with `console.warn('[Auth]`

### Phase 3: Add Development Guard
Create utility:
```typescript
// lib/logger.ts
export const devLog = (...args: unknown[]) => {
  if (process.env.NODE_ENV === 'development') {
    console.log(...args);
  }
};
```

### Phase 4: Production Logging
Consider structured logging for production:
- Use log levels (debug, info, warn, error)
- Add request IDs for tracing
- Consider services like Sentry, LogRocket, or Axiom

---

## Quick Cleanup Commands

```bash
# Count by category (approximate)
grep -rn "console.log.*[🔴🔵🟢🟡🎯📋📄💾📝🖱️🚀⚠️]" --include="*.ts" --include="*.tsx" . | wc -l

# Find STEP pattern
grep -rn "console.log.*\[STEP" --include="*.ts" --include="*.tsx" .

# Find security logs
grep -rn "console.log.*🔒" --include="*.ts" --include="*.tsx" .

# Find inline IIFE debugging
grep -rn "{(() => { console.log" --include="*.tsx" .
```

---

## Files Requiring No Changes

These files have appropriate logging:
- `lib/activity/log.ts` - Uses console.error only for failures
- Most API routes with single auth check logs (after conversion)
