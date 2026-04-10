
# Prose v1.5 - UI Design System
A vanilla CSS library for specific elements/components. We recommend accompanying this with TailwindCSS v4+ for layout and spacing and possible component customization.

Class names are categorized into the following (types are only for reference)
- `component`: root/container/part class
- `part`: container class for nested "parts"
- `modifier`: modifies the component color/size/position/etc.
- `state`: used for manual application hover/focus/disabled/etc, in most cases default HTML states will be be covered by the vanilla CSS.

***

## Config
Include the following CSS files. Use the reset file ONLY if your project does not already include one by default.

- `prs-tokens_v1.5.css`
- `prs-reset_v1.5.css` **OPTIONAL**: use only if your project does not already include a reset
- `prs-styles_v1.5.css`

Always use the CSS variables/tokens in the `prs-tokens_v1.5.css` file where feasible.

***

## Components
### Accordion
Vertically stacked list of items, each item can be expanded or collapsed to reveal the content associated with that item.

**Classes:**
- `.prs-accordion` - component: Container
- `.prs-accordion-content` - part: For content container

**Example:**
```html
<div class="prs-accordion">
  <details>
    <summary>{title}</summary>
    <div class="prs-accordion-content">{content}</div>
  </details>
</div>
```
### Alert
Message box that provides important information to the user, such as warnings, errors, or other notifications.

**Classes:**
- `.prs-alert` - component: Container
- `.prs-alert-success` - modifier: Green variant
- `.prs-alert-toast` - modifier: Floating alert
- `.prs-alert-warning` - modifier: Yellow variant
- `.prs-alert-danger` - modifier: Red variant
- `.prs-alert-ghost` - modifier: Ghost variant
- `.prs-alert-content` - part: For content container

**Example:**
```html
<div class="prs-alert {MODIFIER}" role="alert">
  <div class="icon" aria-hidden="true"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#content-type-info-outline" /></svg></div>
  <div class="prs-alert-content">{content}</div>
  <button class="close" aria-label="Close"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#nav-x" /></svg></button>
</div>
```
### Avatar
🚧 **WORK IN PROGRESS:** Used to show a thumbnail representation of an individual or business in the interface. 🚧

**Classes:**
- `.prs-avatar` - component: Container
- `.prs-avatar-xs` - modifier: Extra-Small variant
- `.prs-avatar-sm` - modifier: Small variant
- `.prs-avatar-md` - modifier: Medium variant
- `.prs-avatar-lg` - modifier: Large variant
- `.prs-avatar-xl` - modifier: Extra-Large variant
- `.prs-avatar-2xl` - modifier: 2x Extra-Large variant
- `.prs-avatar-offline` - modifier: Offline gray dot variant
- `.prs-avatar-online` - modifier: Online green dot variant
- `.prs-avatar-placeholder` - part: For text

**Example:**
```html
<div class="prs-avatar {MODIFIER}">{content: img/svg/.prs-avatar-placeholder}</div>
```
### Badge
Small count or label that appears on another element, often used to display notifications or status information.

**Classes:**
- `.prs-badge` - component: Container
- `.prs-badge-info` - modifier: Aqua variant
- `.prs-badge-success` - modifier: Green variant
- `.prs-badge-warning` - modifier: warning variant
- `.prs-badge-danger` - modifier: Red variant
- `.prs-badge-current` - modifier: Border and text color is inherited
- `.prs-badge-pill` - modifier: Full radius
- `.prs-badge-sharp` - modifier: No radius

**Example:**
```html
<div class="prs-badge {MODIFIER}">{content}</div>
```
### Breadcrumb
Navigation aid that helps users understand their location within a website&#39;s hierarchy and navigate back to previous sections.

**Classes:**
- `.prs-breadcrumb` - component: For &lt;nav&gt; then nest &lt;ol&gt;

**Example:**
```html
<nav class="prs-breadcrumb" role="navigation" aria-label="{label}">
  <ol>
    <li><a href="/">{title}</a></li>
    <li><a href="../../">{title}</a></li>
    <li><a href="../">{title}</a></li>
    <li>{title}</li>
  </ol>
</nav>
```
### Button
Interactive element that users can click to perform an action or navigate to another page.

**Classes:**
- `.prs-btn` - component: For &lt;button&gt; or &lt;a&gt;
- `.prs-btn-primary` - modifier: Contained variant
- `.prs-btn-secondary` - modifier: Outlined variant
- `.prs-btn-tertiary` - modifier: Ghost-like variant
- `.prs-btn-success` - modifier: Green variant
- `.prs-btn-danger` - modifier: Red variant
- `.prs-btn-sm` - modifier: Small variant
- `.prs-btn-lg` - modifier: Large variant
- `.prs-btn-square` - modifier: Square variant
- `.prs-btn-circle` - modifier: Circle variant
- `.prs-btn_hover` - state: Manually apply visual hover
- `.prs-btn_focus` - state: Manually apply visual focus
- `.prs-btn_disabled` - state: Manually apply visual disabled

**Example:**
```html
<button class="btn {MODIFIER}">{label}</button>
```
### Card
Flexible and extensible content container with multiple variants and options.

**Classes:**
- `.prs-card` - component: Container
- `.prs-card-bordered` - modifier: Adds a border
- `.prs-card-action` - modifier: Add some dividers
- `.prs-card-collapse` - modifier: Collapsible
- `.prs-card-indent` - modifier: Collapsible indent
- `.prs-card-header` - part: Container for header
- `.prs-card-title` - part: Container for title
- `.prs-card-body` - part: Container for body (only for -collapse)
- `.prs-card-content` - part: Container for content

**Example:**
```html
<div class="prs-card {MODIFIER}">
  <div class="prs-card-header">
    <div class="prs-card-title">{title}</div>
  </div>
  <div class="prs-card-content">
    {content}
  </div>
  <!-- optional -->
  <div class="prs-card-header">{actions}</div>
</div>
```
### Chat
🚧 **WORK IN PROGRESS:** Used to show conversation and all its data, including the author image, author name, time, etc. 🚧

**Classes:**
- `.prs-chat` - component: Container
- `.prs-chat-start` - modifier: Start aligned
- `.prs-chat-end` - modifier: End aligned
- `.prs-chat-bubble` - part: Message container
- `.prs-chat-image` - part: Optional image/avatar
- `.prs-chat-header` - part: Optional header
- `.prs-chat-footer` - part: Optional footer

**Example:**
```html
<div class="prs-chat {MODIFIER}">
  <!-- optional --> <div class="prs-chat-image prs-avatar prs-avatar-md"><img src="https://placehold.net/4.png" alt="Avatar" /></div>
  <!-- optional --> <div class="prs-chat-header"> <time></time></div>
  <div class="prs-chat-bubble {MODIFIER}">{content}</div>
  <!-- optional --> <div class="prs-chat-footer"></div>
</div>
```
### Checkbox
Form element that allows users to select one or more options from a set.

**Classes:**
- `.prs-checkbox` - component: For &lt;input&gt;
- `.prs-checkbox-label` - component: For &lt;label&gt;
- `.prs-checkbox_indeterminate` - state: Manually apply indeterminate
- `.prs-checkbox_focus` - state: Manually apply focus

**Example:**
```html
<label class="prs-checkbox-label">
  <input type="checkbox" class="prs-checkbox" />
  <span class="prs-label-text">{label}</span>
</label>
```
### Chip
Small, interactive element that represents an input, attribute, or action.

**Classes:**
- `.prs-chip` - component: Container
- `.prs-chip-label` - part: Container
- `.prs-chip_active` - state: Active/Selected
- `.prs-chip_hover` - state: Manually apply visual hover
- `.prs-chip_focus` - state: Manually apply visual focus
- `.prs-chip_disabled` - state: Manually apply visual disabled

**Example:**
```html
<div class="prs-chip {MODIFIER}">
  <span class="prs-chip-label">{label}</span>
</div>
```
### Datepicker
Form element that allows users to select a date from a calendar interface.

**Classes:**
- `.prs-date` - component: For &lt;input&gt;
- `.prs-cal` - component: Container
- `.prs-cal-header` - part: Container
- `.prs-cal-prev` - part: For &lt;button&gt;
- `.prs-cal-next` - part: For &lt;button&gt;
- `.prs-cal-my` - part: For current m/y
- `.prs-cal-days` - part: Day list
- `.prs-cal-week` - part: Weekday list
- `.prs-cal-day` - part: For &lt;button&gt;
- `.prs-cal-day_today` - state: Today
- `.prs-cal-day_selected` - state: Selected day

**Example:**
```html
<div class="prs-cal">
  <div class="prs-cal-header">
    <button class="prs-cal-prev" aria-label="Previous month"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#caret-left" /></svg></button>
    <button class="prs-cal-next" aria-label="Next month"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#caret-right" /></svg></button>
    <span class="prs-cal-my">{month} {year}</span>
  </div>
  <div class="prs-cal-days">
    <div class="prs-cal-week">
      <span>{weekday}</span>
      ...
    </div>
    <button class="prs-cal-day {MODIFER}" aria-label="Mm DD, YYYY">{day}</button>
    ...
  </div>
</div>
```
### Dialog
Modal window that prompts the user to take an action or provides important information.

**Classes:**
- `.prs-dialog` - component: Container
- `.prs-dialog-bordered` - modifier: Divide the header, body, and actions
- `.prs-dialog-box` - part: Houses header, body, action
- `.prs-dialog-header` - part: Houses title and close gadget
- `.prs-dialog-body` - part: Main content
- `.prs-dialog-action` - part: Optional actions
- `.prs-dialog-backdrop` - part: Optional click-to-close

**Example:**
```html
<dialog id="dialog_{id}" class="prs-dialog {MODIFIER}">
  <div class="prs-dialog-box">
    <div class="prs-dialog-header">
      <h2>{title}</h2>
      <button onclick="this.closest('dialog').close()" aria-label="Close" class="prs-dialog-close"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#nav-x" /></svg></button>
    </div>
    <div class="prs-dialog-body">{content}</div>
    <div class="prs-dialog-action">
      <button class="prs-btn prs-btn-secondary" onclick="this.closest('dialog').close()">{secondary}</button>
      <button class="prs-btn prs-btn-primary">{primary}</button>
    </div>
  </div>
  <form method="dialog" class="prs-dialog-backdrop"><button>close</button></form>
</dialog>
```
### Dropdown
Form-like element that allows users to select an option from a list of choices.

**Classes:**
- `.prs-dropdown` - component: Container
- `.prs-menu` - component: For &lt;ul&gt;
- `.prs-menu-item` - part: For &quot;button&quot; container
- `.prs-menu-item-label` - part: For label within &quot;button&quot;
- `.prs-menu-icon` - part: For icon wrapper within &quot;button&quot;

**Example:**
```html
<ul class="prs-menu">
  <li>
    <button class="prs-menu-item">
      <span class="prs-menu-item-label" aria-label="{title}" title="{title}">{title}</span>
      <span class="prs-menu-icon" aria-label="Selected"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#status-check" /></svg></span>
    </button>
  </li>
  ...
</ul>
```
### Form Control
🚧 **WORK IN PROGRESS:** Label positions and fieldset group options. 🚧

**Classes:**
- `.prs-form-control` - component: Container for &lt;label&gt;
- `.prs-form-control-col` - component: Column container for &lt;label&gt;
- `.prs-label` - part: Label styles
- `.prs-label-alt` - part: For use within the column container
- `.prs-label-text` - part: Label text styles
- `.prs-label-text-alt` - part: For use within the column container

**Example:**
```html
<label class="prs-form-control">
  <div class="prs-label"><span class="prs-label-text">{label}</span></div>
  {input}
</label>
```
### Input
Form element that allows users to input and edit text or data into a website page.

**Classes:**
- `.prs-input` - component: For &lt;input&gt; or &lt;label&gt;
- `.prs-input-ghost` - modifier: Remove border
- `.prs-input_focus` - state: Manually apply visual focus
- `.prs-input_invalid` - state: Manually apply visual invalid
- `.prs-input_disabled` - state: Manually apply visual disabled

**Example:**
```html
<input type="{type}" class="prs-input {MODIFIER}" placeholder="{placeholder}" aria-label="{label}" />
```
### Join
🚧 **WORK IN PROGRESS:** A CSS utility component that allows you to join two or more elements together. This looks best when the items have borders or background colors. 🚧

**Classes:**
- `.prs-join` - component: Container
- `.prs-join-vertical` - modifier: Stacked
- `.prs-join-item` - part: Child container

**Example:**
```html
<div class="prs-join {MODIFIER}">
  <button class="prs-join-item">{label}</button>
  <button class="prs-join-item">{label}</button>
  <button class="prs-join-item">{label}</button>
</div>
```
### Loading
Page or container loading indicators.

**Classes:**
- `.prs-loading` - component: Container
- `.prs-loading-reverse` - modifier: Light on dark
- `.prs-loading-xs` - modifier: Size
- `.prs-loading-sm` - modifier: Size
- `.prs-loading-md` - modifier: Size
- `.prs-loading-lg` - modifier: Size
- `.prs-loading-xl` - modifier: Size

**Example:**
```html
<span class="prs-loading {MODIFIER}">
  
</span>
```
### Pagination
Navigation aid that divides content into discrete pages, allowing users to navigate through large sets of data.

**Classes:**
- `.prs-pagination` - component: Container
- `.prs-pagination-pager` - part: Page navigation
- `.prs-pagination-pager_disabled` - state: Page navigation disabled

**Example:**
```html
<nav class="prs-pagination" role="navigation" aria-label="Pagination">
  <ul>
    <li class="prs-pagination-pager prs-pagination-pager_disabled"><a href="#" aria-label="Previous Page"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#chevron-left" /></svg></a></li>
    <li><a href="#" aria-label="Current Page, Page {int}" aria-current="true" aria-label="Go to Page {int}">{int}</a></li>
    <li><a href="#" aria-label="Go to Page {int}">{int}</a></li>
    <li class="prs-pagination-pager"><a href="#" aria-label="Next Page"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#chevron-right" /></svg></a></li>
  </ul>
</nav>
```
### Progress
Visually represents the completion status of a task, process, or page load status.

**Classes:**
- `.prs-progress` - component: Container
- `.prs-progress-radial` - component: Container
- `.prs-progress-label` - component: Container

**Example:**
```html
<progress class="prs-progress" value="{int}" max="{int}">{int}{unit}</progress>
```
### Radio
Form element that allows users to select one option from a group of choices.

**Classes:**
- `.prs-radio` - component: For &lt;input&gt;
- `.prs-radio-label` - component: For &lt;label&gt;
- `.prs-radio_focus` - state: Manually apply visual focus

**Example:**
```html
<label class="prs-radio-label">
  <input type="radio" name="radio_group" class="prs-radio" aria-label="{label}" />
  <span class="prs-label-text">{label}</span>
</label>
```
### Range
A range input allows users to select a value from a specified range.

**Classes:**
- `.prs-range` - component: For &lt;input&gt; or &lt;label&gt;
- `.prs-range-info` - modifier: Blue variant
- `.prs-range-success` - modifier: Green variant
- `.prs-range-warning` - modifier: Yellow variant
- `.prs-range-danger` - modifier: Red variant
- `.prs-range_focus` - state: Manually apply visual focus
- `.prs-range_disabled` - state: Manually apply visual disabled

**Example:**
```html
<label><input type="range" min="{int}" max="{int}" value="{int}" class="prs-range" aria-label="{label}" /></label>
```
### Separator
🚧 **WORK IN PROGRESS:** A visual way to separate sections of content or elements either horizontally or vertically. 🚧

**Classes:**
- `.prs-separator` - component: For container
- `.prs-separator-vertical` - modifier: Flow vertically

**Example:**
```html
<div class="prs-separator {MODIFIER}">{title}</div>
```
### Tab
Navigation aid that allows users to switch between different sections or views within the same page.

**Classes:**
- `.prs-tabs` - component: Container
- `.prs-tabs-center` - modifier: Justify center
- `.prs-tab` - part: For &lt;button&gt;
- `.prs-tab_active` - state: Currently active

**Example:**
```html
<div role="tablist" class="prs-tabs {MODIFIER}">
  <button id="{id}" aria-selected="{bool}" class="prs-tab {MODIFIER}" role="tab">
    {title}
    <!-- optional -->
    <span class="prs-badge">{int}</span>
  </button>
</div>
```
### Table
Element that displays tabular data in a structured format of rows and columns.

**Classes:**
- `.prs-table-container` - component: Container
- `.prs-table` - component: For &lt;table&gt;
- `.prs-table-bordered` - modifier: Add divider lines
- `.prs-table-striped` - modifier: Even/odd highlight
- `.prs-table-compact` - modifier: Less padding
- `.prs-table-pin-rows` - modifier: Sticky &lt;thead&gt; and &lt;tfoot&gt;
- `.prs-table-pin-cols` - modifier: Sticky &lt;th&gt; columns
- `.prs-cell-sort` - modifier: Sortable
- `.prs-cell-name` - modifier: Name/email
- `.prs-cell-stacked` - modifier: Stacked content
- `.prs-cell-end` - modifier: Justify end/right
- `.prs-cell-actions` - part: Header cell actions container
- `.prs-cell-info` - part: Info tooltip container
- `.prs-cell-sort` - part: Sorting container

**Example:**
```html
<div class="prs-table-container">
  <table class="prs-table {MODIFIER}">
    <thead>
      <tr>
        <th>{header}</th>
        ...
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>{cell}</td>
        ...
      </tr>
      ...
    </tbody>
  </table>
</div>
```
### Toggle
Form element that allows users to switch between two states, such as on and off.

**Classes:**
- `.prs-toggle` - component: For &lt;input&gt;
- `.prs-toggle-label` - component: For &lt;label&gt;
- `.prs-toggle-info` - modifier: Red variant
- `.prs-toggle-success` - modifier: Green variant
- `.prs-toggle-warning` - modifier: Yellow variant
- `.prs-toggle-danger` - modifier: Red variant
- `.prs-toggle-neutral` - modifier: Gray variant
- `.prs-toggle-sm` - modifier: Small size
- `.prs-toggle_focus` - state: Manually apply visual focus
- `.prs-toggle_disabled` - state: Manually apply visual disabled

**Example:**
```html
<label><input type="checkbox" class="prs-toggle {MODIFIER}" aria-label="{label}" /></label>
```
