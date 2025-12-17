# NotebookLM UI Quick Reference

## Interface Layout

```
┌─────────────────────────────────────────────────────────────────┐
│  NotebookLM                                            Settings │
├──────────────────┬──────────────────────────┬───────────────────┤
│   LEFT SIDEBAR   │      CENTER AREA         │   RIGHT PANEL     │
│                  │                          │                   │
│  ┌────────────┐  │                          │   Studio          │
│  │ Search box │  │   Main content area      │                   │
│  │ (AVOID!)   │  │   or Modal dialogs       │   - Audio Overview│
│  └────────────┘  │                          │   - Video Overview│
│                  │   ┌──────────────────┐   │   - Mind Map      │
│  Sources list    │   │  MODAL DIALOG    │   │   - Reports       │
│  - Source 1      │   │                  │   │   - Flashcards    │
│  - Source 2      │   │  ┌────────────┐  │   │   - Quiz          │
│                  │   │  │  INPUT     │  │   │                   │
│  [Add sources]   │   │  │  (TARGET!) │  │   │                   │
│                  │   │  └────────────┘  │   │                   │
│                  │   │                  │   │                   │
│                  │   │  [Insert]        │   │                   │
│                  │   └──────────────────┘   │                   │
└──────────────────┴──────────────────────────┴───────────────────┘
```

## Selector Cheat Sheet

### Textareas (CRITICAL)

| Purpose | Placeholder | Class Contains | ID Pattern |
|---------|-------------|----------------|------------|
| URL input (CORRECT) | `Paste any links` | - | `mat-input-X` |
| Text paste (CORRECT) | `Paste text here` | `copied-text-input` | `mat-input-X` |
| Sidebar search (AVOID) | `Search the web` | `query-box` | `mat-input-0` |
| Chat input (AVOID) | `Start typing` | - | - |

### Buttons

| Button | Text Content |
|--------|--------------|
| Create notebook | `Create new` |
| Add sources | `Add sources` |
| Source type - web | `Websites` |
| Source type - text | `Copied text` |
| Submit | `Insert` |

## Modal Detection

```javascript
// Check if modal is open
var modals = document.querySelectorAll('[role="dialog"], .mat-mdc-dialog-container');
var isModalOpen = modals.length > 0;

// Identify modal type
if (document.querySelector('textarea[placeholder*="Paste any links"]')) {
    // URL input modal
} else if (document.querySelector('textarea[placeholder="Paste text here"]')) {
    // Text paste modal
}
```

## Common Mistakes

### 1. Wrong Textarea

```javascript
// ❌ WRONG - grabs first textarea (sidebar search)
document.querySelector('textarea')

// ✅ CORRECT - specific selector
document.querySelector('textarea[placeholder="Paste any links"]')
```

### 2. No Event Dispatch

```javascript
// ❌ WRONG - Angular doesn't detect change
textarea.value = 'content';

// ✅ CORRECT - triggers Angular validation
var setter = Object.getOwnPropertyDescriptor(HTMLTextAreaElement.prototype, 'value').set;
setter.call(textarea, 'content');
textarea.dispatchEvent(new Event('input', {bubbles: true}));
```

### 3. Clicking Disabled Button

```javascript
// ❌ WRONG - might be disabled
button.click();

// ✅ CORRECT - check first
if (!button.disabled && !button.className.includes('disabled')) {
    button.click();
}
```

## Debug Helper

```javascript
// Log all textareas to identify the right one
Array.from(document.querySelectorAll('textarea')).forEach((t, i) => {
    console.log(i, {
        placeholder: t.placeholder,
        class: t.className.substring(0, 40),
        value: t.value.substring(0, 30),
        visible: t.offsetParent !== null
    });
});
```
