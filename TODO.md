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

### Transparency & Debugging
- [ ] **Verbose Logging Mode**: Add a `debug: true` option to tools that logs detailed information about the DOM traversal, event dispatching, and any errors encountered during execution to

- [] Make it so that if active that there is a visiual indicator in the browser that the tool is active and what it is doing (e.g. a small overlay in the corner that says "HaknErd Active: Clicking Button" or "HaknErd Active: Typing in Input"). This would help with debugging and also make it clear to users when the tool is interacting with the page. And also prevent user from entering stuff while the tool is active and potentially messing up the tool's actions. and also add button to the overlay that allows user to immediately stop the tool if they see it doing something they don't want.

- [ ] **Error Reporting**: When a tool fails (e.g. element not found, timeout), return a structured error object with details about what was attempted, what was found in the DOM, and any relevant console logs or network activity to aid debugging.

- [ ] **Performance Metrics**: Collect and return performance metrics (e.g. time taken for each step, number of DOM nodes traversed) with each tool execution to help identify bottlenecks and optimize future improvements.

- [ ] reduce token usage by implementing a more efficient way to represent the DOM in the context window, such as a compressed or summarized version that still allows for effective querying and interaction without needing to include the entire DOM structure.

- [ ] better connected state display in the UI, such as showing which browser instance is currently active and connected, and allowing users to easily switch between multiple instances if needed. This would improve the user experience and make it clearer when the tool is actively controlling a browser.



### State Management & Token Conservation
- [ ] **DOM Diffing / Delta Updates**: Instead of pulling the entire page text/snapshot after every action, capture the state before the interaction and only return the *delta* (what elements or text were added, removed, or changed). This will massively conserve LLM context tokens and make it easier to see the immediate result of an action.
