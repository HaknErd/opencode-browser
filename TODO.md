# HaknErd Browser TODO List

## Current Limitations & Future Improvements

### Core Interactions
- [ ] **Cross-Origin iframe Support**: Update tools (`browser_click`, `browser_type`, `browser_query`) to correctly traverse and interact with elements inside nested, cross-origin iframes.
- [ ] **Advanced Shadow DOM Piercing**: Currently `browser_eval` can be used as a workaround, but `browser_query` and `browser_click` should have an automatic mechanism (or a dedicated `pierce: true` parameter) to recursively find deeply nested shadow elements.
- [ ] **Drag and Drop**: Implement a `browser_drag` tool that dispatches precise mouse events for standard drag-and-drop interactions.

### Reliability & Stealth
- [ ] **Bot Detection Evasion**: Add random jitter to `pollMs` and typing intervals to bypass heuristic bot detection like reCAPTCHAs. 
- [ ] **Native Clicks**: Shift from JS `element.click()` to Chrome Debugger protocol (`Input.dispatchMouseEvent`) clicks when `chrome.debugger` is attached to simulate true hardware clicks.

### Browser State & Lifecycle
- [ ] **New Window Claiming**: Improve the broker logic so it can automatically claim popup windows spawned by a click, not just new tabs in the same window.
- [ ] **Persistent Auth**: Add capabilities to store and inject cookies/localStorage from previous sessions to maintain authenticated states between runs.
- [ ] **Page Readiness Triggers**: Instead of relying solely on `timeoutMs` or specific `waitFor*` attributes, implement an automatic heuristic based on network idle time (via DevTools protocol) before returning a click/navigate result.

### Developer Experience (DX)
- [ ] **Interactive Tool Tests**: Create an automated test suite (using `bin/tool-test.ts`) that runs locally to prevent regressions.
- [ ] **Refine `browser_snapshot`**: The current recursive DOM extraction works well but truncates output heavily on massive pages. Implement a paginated or "element-focused" snapshot that allows deeper inspection without blowing up the context window.
