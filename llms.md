
# Prose UI - UI Design System
A vanilla CSS library for specific elements/components. We recommend accompanying this with TailwindCSS v4+ for layout and spacing and possible component customization.

Class names are categorized into the following (types are only for reference)
- `component`: root/container/part class
- `part`: container class for nested "parts"
- `modifier`: modifies the component color/size/position/etc.
- `state`: used for manual application hover/focus/disabled/etc, in most cases default HTML states will be be covered by the vanilla CSS.

***

## Config
Include the following CSS files along with TailwindCSS so we have a decent utility framework and a CSS reset.

- `https://cdn.jsdelivr.net/gh/prose-ui/prose-ui@latest/prs-tokens.css`
- `https://cdn.jsdelivr.net/gh/prose-ui/prose-ui@latest/prs-styles.css`

Always use the CSS variables/tokens in the `prs-tokens.css` file where feasible.

***

## Note
The example markup for each component uses Alpine.js. Ideally convert this logic to the syntax of choice by the user. If the user does not prefer a specific syntax, please use Alpine.js for simplicity sake.

***

## Components

### Accordion

**Description**  
Vertically stacked list of items, each item can be expanded or collapsed to reveal the content associated with that item.

**For best accessibility:**  
Please use **details** and **summary** tags. Our CSS takes care of motion-safe sliding open/close animations.

**Classes:**  
- `.prs-accordion` - component: Container
- `.prs-accordion-content` - part: For content container

**Example:**  
```html
<div class="w-screen max-w-lg">
  <div class="prs-accordion" :class="{
    'prs-accordion-plus': symbol === 'plus',
    'prs-accordion-ghost': ghost,
  }">
    <details :name="exclusive && 'group-name'" :open="open ? open : false">
      <summary>Summary</summary>
      <div class="prs-accordion-content">
        Lorem ipsum dolor sit amet. Ad aute proident do eu ad eu consectetur ad esse incididunt mollit non.
      </div>
    </details>
    <details :name="exclusive && 'group-name'">
      <summary>Here's a summary with a very long label so we can test the wrapping and make sure the icon position, flex gap, and flex-shrink rules are working properly</summary>
      <div class="prs-accordion-content">
        Lorem ipsum dolor sit amet. Ad aute proident do eu ad eu consectetur ad esse incididunt mollit non.
      </div>
    </details>
    <details :name="exclusive && 'group-name'">
      <summary>The third summary</summary>
      <div class="prs-accordion-content">
        Lorem ipsum dolor sit amet. Ad aute proident do eu ad eu consectetur ad esse incididunt mollit non.
      </div>
    </details>
  </div>
</div>
```

***

### Alert

**Description**  
Message box that provides important information to the user, such as warnings, errors, or other notifications.

**For best accessibility:**  
Please use **role** and **aria-live** attributes depending on your use case.

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
<div class="w-96 max-w-xs">
  <div
    role="alert"
    class="prs-alert"
    :class="{
      'prs-alert-info': variant === 'info',
      'prs-alert-success': variant === 'success',
      'prs-alert-warning': variant === 'warning',
      'prs-alert-danger': variant === 'danger',
      'prs-alert-neutral': variant === 'neutral',
      'prs-alert-ghost': ghost,
    }"
  >
    <div x-show="withIcon" class="icon" aria-hidden="true" style="display: none">
      <iconify-icon :icon="variant === 'success'  ? 'mdi:check-circle-outline' :
        variant === 'warning' ? 'mdi:warning-outline' :
        variant === 'danger' ? 'mdi:cancel' :
        'mdi:information-outline'" noobserver></iconify-icon>
    </div>
    <div class="prs-alert-content"><span x-text="variant" class="capitalize"></span> message slot...</div>
    <button x-show="withClose" class="close" aria-label="Close" style="display: none">
      <iconify-icon icon="mdi:close" noobserver></iconify-icon>
    </button>
  </div>
</div>
```

***

### Attachment

**Description**  
Attached files to messages or file type input.

**Classes:**  
- `.prs-attachment` - component: Container
- `.prs-thumb` - part: Thumbnail container (img, svg, iconify-icon)
- `.prs-meta` - part: Details container
- `.prs-name` - part: file name
- `.prs-ext` - part: file type/ext
- `.prs-close` - part: Close/remove button

**Example:**  
```html
<div class="prs-attachment w-screen max-w-xs">
  <div class="prs-thumb">
    <svg x-show="!thumbnail" xmlns="http://www.w3.org/2000/svg" width="24" height="24" role="img" fill="currentColor">
      <use href="/_assets/prs-icons.svg#content-type-blank-document"></use>
    </svg>
    <img x-show="thumbnail" src="https://placehold.net/4.png" alt="File thumbnail preview" />
  </div>
  <div class="prs-meta">
    <div class="prs-name" x-text="name.length ? name : 'file_name.png'"></div>
    <small class="prs-ext" x-text="extension"></small>
  </div>
  <button x-show="withRemove" class="prs-close"><iconify-icon icon="mdi:close" noobserver></iconify-icon></button>
</div>
```

***

### Avatar

**Description**  
Used to show a thumbnail representation of an individual or business in the interface.

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
<div
  class="prs-avatar"
  :class="{
    'prs-avatar-xs': size === 'xs',
    'prs-avatar-sm': size === 'sm',
    'prs-avatar-md': size === 'md',
    'prs-avatar-lg': size === 'lg',
    'prs-avatar-xl': size === 'xl',
    'prs-avatar-2xl': size === '2xl',
    'prs-avatar-online': status,
  }"
>
  <img x-show="variant === 'image'" src="https://placehold.net/4.png" alt="Avatar component" />
  <iconify-icon x-show="variant === 'icon'" icon="mdi:account" width="100%" height="100%" noobserver></iconify-icon>
  <span x-show="variant === 'initials'" class="prs-avatar-placeholder">WW</span>
</div>
```

***

### Badge

**Description**  
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
<span
  class="prs-badge max-w-80"
  :class="{
    'prs-badge-info': variant === 'info',
    'prs-badge-success': variant === 'success',
    'prs-badge-warning': variant === 'warning',
    'prs-badge-danger': variant === 'danger',
    'prs-badge-current': variant === 'current',
    'prs-badge-pill': shape === 'pill',
    'prs-badge-sharp': shape === 'sharp',
  }"
>
  <span x-text="text ? text : 'Badge'" class="line-clamp-1 pointer-events-none"></span>
</span>
```

***

### Breadcrumb

**Description**  
Navigation aid that helps users understand their location within a website&#39;s hierarchy and navigate back to previous sections.

**For best accessibility:**  
Please use **nav** with nested **ol** tags as well as  **role=&quot;navigation&quot;** and **aria-label** attributes.

**Classes:**  
- `.prs-breadcrumb` - component: For &lt;nav&gt; then nest &lt;ol&gt;

**Example:**  
```html
<nav class="prs-breadcrumb" role="navigation" aria-label="Breadcrumbs">
  <ol>
    <li><a @click.prevent href="/" title="Home">Home</a></li>
    <li><a @click.prevent href="../../" title="...">Parent with a really long name to see truncation</a></li>
    <li><a @click.prevent href="../" title="Parent">Parent</a></li>
    <li :title="current" x-text="current !== '' ? current : 'Current'"></li>
  </ol>
</nav>
```

***

### Button

**Description**  
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
<button
  class="prs-btn"
  :class="{
    'prs-btn-primary': variant === 'primary',
    'prs-btn-secondary': variant === 'secondary',
    'prs-btn-tertiary': variant === 'tertiary',
    'prs-btn-success': color === 'success',
    'prs-btn-danger': color === 'danger',
    'prs-btn-sm': size === 'sm',
    'prs-btn-lg': size === 'lg',
    'prs-btn-square': shape === 'square',
    'prs-btn-circle': shape === 'circle',
    'prs-btn_hover': state === 'hover',
    'prs-btn_focus': state === 'focus',
  }"
  :disabled="state === 'disabled'"
>
  <iconify-icon x-show="shape !== 'default' || (withIcon === 'leading')" icon="mdi:close" class="icon pointer-events-none" noobserver></iconify-icon>
  <span x-show="shape === 'default'" x-text="text ? text : 'Button'" class="line-clamp-1 pointer-events-none"></span>
  <iconify-icon x-show="(withIcon === 'trailing' && shape === 'default')" icon="mdi:close" class="icon pointer-events-none" noobserver></iconify-icon>
</button>
```

***

### Card

**Description**  
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
<div x-data="{ expanded: true }" class="prs-card w-screen max-w-lg" :class="{
  'prs-card-bordered': bordered,
  'prs-card-action': action,
  'prs-card-collapse': collapse,
  'prs-card-indent': collapseIndent,
}">
  <a x-show="collapse" @click.prevent="expanded = !expanded" :aria-expanded="expanded" href="#" class="prs-card-header">
    <div class="icon" aria-hidden="true"><iconify-icon icon="mdi:chevron-right" width="100%" height="100%" class="iconify" noobserver></iconify-icon></div>
    <div class="prs-card-title" x-text="title ? title : 'Card header'"></div>
  </a>
  <div x-show="!collapse" class="prs-card-header">
    <div class="prs-card-title" x-text="title ? title : 'Card header'"></div>
    <button x-show="action" class="prs-btn prs-btn-tertiary">Action</button>
  </div>
  <div x-show="collapse">
    <div x-show="expanded" x-collapse class="prs-card-body">
      <div class="prs-card-content">
        <p x-text="body ? body : 'Lorem ipsum'"></p>
      </div>
    </div>
  </div>
  <div x-show="!collapse" class="prs-card-content">
    <p x-text="body ? body : 'Lorem ipsum'"></p>
  </div>
  <div x-show="action && !collapse" class="prs-card-footer">
    <button class="prs-btn prs-btn-secondary">Action</button>
    <button class="prs-btn prs-btn-primary">Action</button>
  </div>
</div>
```

***

### Chat

**Description**  
Used to show conversation and all its data, including the author image, author name, time, etc.

**For best accessibility:**  
The maximum width of a chat bubble should be around **65ch**. This will ensure the best readability.

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
<div class="w-xl max-w-xs">
  <div
    class="prs-chat prs-chat-start"
    :class="{
      'prs-chat-start': position === 'start',
      'prs-chat-end': position === 'end',
    }"
  >
    <div x-show="avatar" x-transition class="prs-chat-image prs-avatar prs-avatar-md"><img src="https://placehold.net/4.png" alt="Chat bubble component" /></div>
    <div x-show="header" x-transition class="prs-chat-header">Ohbee One <time>12:34</time></div>
    <div
      class="prs-chat-bubble"
      :class="{
        'prs-chat-bubble-primary': variant === 'primary',
        'prs-chat-bubble-secondary': variant === 'secondary',
        'prs-chat-bubble-accent': variant === 'accent',
        'prs-chat-bubble-info': variant === 'info',
        'prs-chat-bubble-success': variant === 'success',
        'prs-chat-bubble-warning': variant === 'warning',
        'prs-chat-bubble-danger': variant === 'danger',
      }"
      x-text="message.length ? message : 'You were the chosen one...'"
    ></div>
    <div x-show="footer" x-transition class="prs-chat-footer">Delivered</div>
  </div>
</div>
```

***

### Checkbox

**Description**  
Form element that allows users to select one or more options from a set.

**Classes:**  
- `.prs-checkbox` - component: For &lt;input&gt;
- `.prs-checkbox-label` - component: For &lt;label&gt;
- `.prs-checkbox_indeterminate` - state: Manually apply indeterminate
- `.prs-checkbox_focus` - state: Manually apply focus

**Example:**  
```html
<label
  class="prs-checkbox-label"
  x-init="
    $watch('checked', value => {
      indeterminate = false;
    });
    $watch('indeterminate', value => {
      $refs.prsCheckbox.indeterminate = value;
    });
  "
>
  <input
    type="checkbox"
    x-model="checked"
    x-ref="prsCheckbox"
    x-init="$el.indeterminate = indeterminate"
    class="prs-checkbox"
    :class="{
      'prs-checkbox-lg': size === 'lg',
      'prs-checkbox-xl': size === 'xl',
      'prs-checkbox_focus': state === 'focus',
    }"
    :disabled="state === 'disabled'" />
  <span x-text="label ? label : 'Label'" class="prs-label-text"></span>
</label>
```

***

### Chip

**Description**  
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
<button
  class="prs-chip"
  :class="{
    'prs-chip_active': variant === 'active',
    'prs-chip_hover': state === 'hover',
    'prs-chip_focus': state === 'focus',
  }"
  :disabled="state === 'disabled'"
>
  <span x-show="icon" x-transition class="icon"><iconify-icon icon="mdi:checkbox-marked" class="iconify text-xl" noobserver></iconify-icon></span>
  <span class="prs-chip-label" x-text="text ? text : 'Text'"></span>
  <span x-show="close" x-transition class="close"><iconify-icon icon="mdi:close" class="iconify" noobserver></iconify-icon></span>
</button>
```

***

### Datepicker

**Description**  
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
<div class="w-96 max-w-[16.875rem]">
  <div class="prs-cal">
    <div class="prs-cal-header">
      <button class="prs-cal-prev" aria-label="Previous month">
        <iconify-icon icon="mdi:menu-left" width="1.5rem" height="1.5rem" noobserver></iconify-icon>
      </button>
      <button class="prs-cal-next" aria-label="Next month">
        <iconify-icon icon="mdi:menu-right" width="1.5rem" height="1.5rem" noobserver></iconify-icon>
      </button>
      <span class="prs-cal-my">Month 20XX</span>
    </div>
    <div class="prs-cal-days">
      <div class="prs-cal-week">
        <span>Sun</span>
        <span>Mon</span>
        <span>Tue</span>
        <span>Wed</span>
        <span>Thu</span>
        <span>Fri</span>
        <span>Sat</span>
      </div>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">26</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">27</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">28</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">29</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">30</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">31</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">1</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">2</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">3</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">4</button>
      <button class="prs-cal-day prs-cal-day_selected" aria-label="Mm DD, YYYY selected">5</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">6</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">7</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">8</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">9</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">10</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">11</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">12</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">13</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">14</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">15</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">16</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">17</button>
      <button class="prs-cal-day prs-cal-day_today" aria-current="date" aria-label="Mm DD, YYYY">18</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">19</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">20</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">21</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">22</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">23</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">24</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">25</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">26</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">27</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">28</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">29</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">30</button>
      <button class="prs-cal-day" aria-label="Mm DD, YYYY">31</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">1</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">2</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">3</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">4</button>
      <button class="prs-cal-day prs-cal-day_disabled" aria-label="Mm DD, YYYY">5</button>
    </div>
  </div>
</div>
```

***

### Dialog

**Description**  
Modal window that prompts the user to take an action or provides important information.

**For best accessibility:**  
Please use the **dialog** tag. It automatically comes with **FREE** accessibility features that are built into the browser and operating system like keyboard controls, focus trap with access to browser controls (react focus trap does NOT support this and is NOT accessible), unlimited dialog nesting/stacking, optional click outside to close, etc.
&lt;br /&gt;&lt;br /&gt;
To prevent **esc ⎋** or click-outside-to-close you can use **closedby=&quot;none|closerequest&quot;**.

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
<div class="absolute inset-0">
  <div id="dialog_id" class="!bg-black/50 prs-dialog !min-w-full !min-h-full !absolute" role="dialog" :class="bordered && 'prs-dialog-bordered'" open>
    <div class="prs-dialog-box !max-h-72">
      <div class="prs-dialog-header">
        <h2 x-text="title ? title : 'Dialog title'" class="line-clamp-1"></h2>
        <button onclick="this.closest('dialog').close()" aria-label="Close" class="prs-dialog-close">
          <iconify-icon icon="mdi:close" class="iconify text-2xl" noobserver></iconify-icon>
        </button>
      </div>
      <div class="prs-dialog-body">
        <p x-text="body ? body : 'Lorem ipsum'"></p>
      </div>
      <div class="prs-dialog-action" :hidden="!withActions">
        <button class="prs-btn prs-btn-secondary" onclick="this.closest('dialog').close()">Secondary</button>
        <button class="prs-btn prs-btn-primary">Primary</button>
      </div>
    </div>
    <form method="dialog" class="prs-dialog-backdrop">
      <button>close</button>
    </form>
  </div>
</div>
```

***

### Dropdown

**Description**  
Form-like element that allows users to select an option from a list of choices.

**Classes:**  
- `.prs-dropdown` - component: Container
- `.prs-menu` - component: For &lt;ul&gt;
- `.prs-menu-item` - part: For &quot;button&quot; container
- `.prs-menu-item-label` - part: For label within &quot;button&quot;
- `.prs-menu-icon` - part: For icon wrapper within &lt;button&gt;

**Example:**  
```html
<div class="prs-dropdown">
  <button class="prs-btn prs-btn-secondary">Dropdown</button>
  <ul class="prs-menu">
    <li><button class="prs-menu-item"><span class="prs-menu-item-label">Menu item</span></button></li>
    <li>
      <button @click.prevent="active = !active" class="prs-menu-item" :class="{
        'prs-menu-item_hover': state === 'hover',
        'prs-menu-item_focus': state === 'focus',
      }">
        <span class="prs-menu-item-label" aria-label="Truncate very long menu item labels" title="Truncate very long menu item labels">Truncate very long menu item labels</span>
        <span x-show="active" class="prs-menu-icon" aria-label="Selected"><iconify-icon icon="mdi:check" width="24px" height="24px" class="iconify" noobserver></iconify-icon></span>
      </button>
    </li>
    <li><button class="prs-menu-item"><span class="prs-menu-item-label">Menu item</span></button></li>
  </ul>
</div>
```

***

### File

**Description**  
Form field input type for uploading files to a web server.

**Note:**  
This is a modifier of **.prs-input**. Please use [input](../input/) properties and then stack **.prs-file**. Use this alongside the [attachment](../attachment/) component.

**Classes:**  
- `.prs-file` - component: Container

**Example:**  
```html
<div x-data="fileUpload()" class="w-screen max-w-md">
  <div class="prs-form-control">
    <input @change="handleFiles" x-ref="fileInput" type="file" id="preview-file" class="prs-input prs-file" :class="{
      'prs-input-ghost': variant === 'ghost',
      'prs-input_hover': state === 'hover',
      'prs-input_focus': state === 'focus',
    }" :disabled="state === 'disabled'" multiple />
  </div>
  <div x-show="files.length" x-transition class="py-3 grid grid-cols-[repeat(auto-fit,minmax(12.5rem,1fr))] gap-3">
    <template x-for="(file, index) in files" :key="file.name" hidden>
      <div class="prs-attachment">
        <div class="prs-thumb"><svg width="24" height="24" role="img" fill="currentColor"><use href="/_assets/prs-icons.svg#content-type-blank-document"></use></svg></div>
        <div class="prs-meta">
          <div class="prs-name" x-text="file.name"></div>
          <small class="prs-ext" x-text="file.type"></small>
        </div>
        <button @click="removeFile(index)" class="prs-close"><iconify-icon icon="mdi:close" noobserver></iconify-icon></button>
      </div>
    </template>
  </div>
</div>
```

***

### Form Control

**Description**  
Label positions and fieldset group options.

**For best accessibility:**  
Make sure your **label** uses a **for** attribute that ties to your input **id** so the user can click on the label to give focus to the input.

**Classes:**  
- `.prs-form-control` - component: Container for &lt;label&gt;
- `.prs-form-control-col` - component: Column container for &lt;label&gt;
- `.prs-label` - part: Label styles
- `.prs-label-alt` - part: For use within the column container
- `.prs-label-text` - part: Label text styles
- `.prs-label-text-alt` - part: For use within the column container.

**Example:**  
```html
<div class="w-screen" :class="column ? 'max-w-3xl' : 'max-w-xs'"> <!-- <- this is just for demo purposes -->
  <div :class="column ? 'prs-form-control-col' : 'prs-form-control'">
    <div class="prs-label" :class="column && 'prs-label-col'">
      <label :for="'input-'+ input" class="prs-label-text" x-text="label"></label>
      <span x-show="showAlt" class="prs-label-text" :class="column && 'prs-label-text-sub'" x-text="column ? 'Some sub text to better instruct the user on how to fill out the fieldset.' : 'Alt'"></span>
    </div>
    <div class="prs-form-control">
      <input x-show="input === 'text'" type="text" :id="'input-'+ input" class="prs-input" placeholder="Input" />
      <select x-show="input === 'select'" :id="'input-'+ input" class="prs-input prs-select"><option selected disabled>Choose:</option></select>
      <textarea x-show="input === 'textarea'" :id="'input-'+ input" class="prs-input" placeholder="Textarea"></textarea>
      <template x-for="i in 3" :key="input +'-'+ i">
        <label x-show="input === 'radios'" class="prs-radio-label"><input type="radio" :id="i === 1 ? ('input-'+ input) : false" name="myRadios" class="prs-radio" /> <span class="prs-label-text">Some label</span></label>
      </template>
      <template x-for="i in 3" :key="input +'-'+ i">
        <label x-show="input === 'checkboxes'" class="prs-checkbox-label"><input type="checkbox" :id="i === 1 ? ('input-'+ input) : false" class="prs-checkbox" /> <span class="prs-label-text">Some label</span></label>
      </template>
      <div x-show="input === 'toggle'">
        <label class="prs-toggle-label">
          <input type="checkbox" :id="'input-'+ input" class="prs-toggle" />
          <!-- <span class="prs-label-text">Toggle</span> -->
        </label>
      </div>
      <div class="prs-label">
        <span x-show="showAlt || showValidated" class="prs-label-text" :class="showValidated && 'prs-label-error'" x-text="showValidated ? 'Validation message' : 'Alt'"></span>
        <span x-show="showAlt" class="prs-label-text">Alt</span>
      </div>
    </div>
  </div>
</div>
```

***

### Input

**Description**  
Form element that allows users to input and edit text or data into a website page.

**Classes:**  
- `.prs-input` - component: For &lt;input&gt; or &lt;label&gt;
- `.prs-input-ghost` - modifier: Remove border
- `.prs-input_focus` - state: Manually apply visual focus
- `.prs-input_invalid` - state: Manually apply visual invalid
- `.prs-input_disabled` - state: Manually apply visual disabled

**Example:**  
```html
<label class="prs-form-control w-screen max-w-xs">
  <input
    x-model="value"
    x-show="type !== 'select' && type !== 'textarea'"
    @focus="$el.showPicker()"
    :type="type"
    :class="{
      'prs-input-ghost': variant === 'ghost',
      'prs-input_focus': state === 'focus',
      'prs-input_invalid': invalid,
      'prs-select': type === 'select',
      'prs-textarea': type === 'textarea',
      'prs-file': type === 'file',
    }"
    :placeholder="placeholder ? placeholder : 'Text Placeholder'"
    :disabled="state === 'disabled'"
    class="prs-input"
  />
  <textarea
    x-show="type === 'textarea'"
    x-model="value"
    :class="{
      'prs-input-ghost': variant === 'ghost',
      'prs-input_focus': state === 'focus',
      'prs-input_invalid': invalid,
    }"
    :placeholder="placeholder ? placeholder : 'Textarea Placeholder'"
    :disabled="state === 'disabled'"
    class="prs-input"
  ></textarea>
  <select
    x-show="type === 'select'"
    :disabled="state === 'disabled'"
    :class="{
      'prs-input-ghost': variant === 'ghost',
      'prs-input_focus': state === 'focus',
      'prs-input_invalid': invalid,
    }"
    class="prs-input prs-select"
  >
    <option selected disabled>Choose:</option>
    <option>Option 1</option>
    <option>Option 2</option>
    <option>Option 3</option>
  </select>
  <span class="prs-label-text prs-label-error">Error message</span>
</div>
```

***

### Join

**Description**  
A utility that allows you to join two or more elements together. This looks best when the items have borders or background colors.

**Classes:**  
- `.prs-join` - component: Container
- `.prs-join-vertical` - modifier: Stacked
- `.prs-join-item` - part: Child container

**Example:**  
```html
<div
  x-show="!complex"
  :class="{
    'prs-join-vertical': orientation === 'vertical',
  }"
  class="prs-join"
  style="display: none;"
>
  <button class="prs-btn prs-btn-secondary prs-btn-square prs-join-item"><iconify-icon icon="mdi:format-align-left" noobserver></iconify-icon></button>
  <button class="prs-btn prs-btn-secondary prs-btn-square prs-join-item"><iconify-icon icon="mdi:format-align-center" noobserver></iconify-icon></button>
  <button class="prs-btn prs-btn-secondary prs-btn-square prs-join-item"><iconify-icon icon="mdi:format-align-right" noobserver></iconify-icon></button>
</div>

<div
  x-show="complex"
  :class="{
    'prs-join-vertical': orientation === 'vertical',
  }"
  class="prs-join mx-auto w-screen max-w-xs"
  style="display: none;"
>
  <div>
    <label><input type="search" class="prs-input prs-join-item" placeholder="Search" aria-label="Search query" /></label>
  </div>
  <label>
    <select class="prs-input prs-select prs-join-item w-auto" :class="orientation === 'horizontal' && 'max-w-[6.25rem]'" aria-label="Filter option">
      <option disabled selected>Filter</option>
      <option>Title</option>
      <option>Genre</option>
    </select>
  </label>
  <button class="prs-btn prs-btn-primary prs-join-item" :class="orientation === 'horizontal' && 'prs-btn-square'" aria-label="Search">
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img">
      <use href="/_assets/prs-icons.svg#nav-search" />
    </svg>
  </button>
</div>
```

***

### Loading

**Description**  
Page or container loading indicators.

**Note:**  
If the user has reduce motion settings applied in their browser or OS the spin animation changes to a subtle fader.

**Classes:**  
- `.prs-loading` - component: Container
- `.prs-loading-fade` - modifier: Force the fade animation
- `.prs-loading-reverse` - modifier: Light on dark
- `.prs-loading-xs` - modifier: Size
- `.prs-loading-sm` - modifier: Size
- `.prs-loading-md` - modifier: Size
- `.prs-loading-lg` - modifier: Size
- `.prs-loading-xl` - modifier: Size

**Example:**  
```html
<div class="absolute inset-0 flex items-center justify-center rounded-box transition" :class="reverse && 'bg-black/60'">
  <span
    class="prs-loading"
    :class="{
      'prs-loading-xs': size === 'xs',
      'prs-loading-sm': size === 'sm',
      'prs-loading-md': size === 'md',
      'prs-loading-lg': size === 'lg',
      'prs-loading-xl': size === 'xl',
      'prs-loading-reverse': reverse,
      'prs-loading-fade': motionsafe,
    }"
  >
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 200">
      <defs>
        <mask id="spinner-mask">
          <polygon class="spinner-burst" points="200 103.43 199.98 96.06 132.69 96.23 198.26 81.09 196.6 73.91 131.03 89.05 191.59 59.7 188.37 53.07 127.82 82.42 180.32 40.33 175.71 34.59 123.21 76.67 165.03 23.96 159.26 19.38 117.44 72.09 146.48 11.39 139.83 8.21 110.79 68.91 125.6 3.27 118.41 1.65 103.6 67.29 103.43 0 96.06 .02 96.23 67.31 81.09 1.74 73.91 3.4 89.05 68.97 59.7 8.41 53.07 11.63 82.42 72.18 40.33 19.68 34.59 24.29 76.67 76.79 23.96 34.97 19.38 40.74 72.09 82.56 11.39 53.52 8.21 60.17 68.91 89.21 3.27 74.4 1.65 81.59 67.29 96.4 0 96.57 .02 103.94 67.31 103.77 1.74 118.91 3.4 126.09 68.97 110.95 8.41 140.3 11.63 146.93 72.18 117.58 19.68 159.67 24.29 165.42 76.79 123.33 34.97 176.04 40.74 180.62 82.56 127.91 53.52 188.61 60.17 191.79 89.21 131.09 74.4 196.73 81.59 198.35 96.4 132.71 96.57 200 103.94 199.98 103.77 132.69 118.91 198.26 126.09 196.6 110.95 131.03 140.3 191.59 146.93 188.37 117.58 127.82 159.67 180.32 165.41 175.71 123.33 123.21 176.04 165.03 180.62 159.26 127.91 117.44 188.61 146.48 191.79 139.83 131.09 110.79 196.73 125.6 198.35 118.41 132.71 103.6 200 103.43" />
          <circle class="spinner-center" cx="100" cy="100" r="36" />
        </mask>
      </defs>
      <g class="spinner" mask="url(#spinner-mask)">
        <path class="spinner-shape-1" d="M69.13,24.54c-28.53,7.23-53.33,125.75-16.96,142.83,37.3,17.52,98.5-4.67,111.3-39.04,15.97-42.87-68.32-110.39-94.34-103.79Z" />
        <path class="spinner-shape-2" d="M134.03,159.16s-23.38,11.77-42.45-2.6c-19.06-14.37-141.52-88.35-19.47-107.14,26.27-4.05,32.13-31.14,73.35-16.7,25.79,9.04,44.25,102.01-11.43,126.44Z" />
        <path class="spinner-shape-3" d="M163.47,128.33c12.23-31.33-28.29-73.76-61.41-93.56-9.4,5.42-17.32,12.7-29.95,14.65-10.41,1.6-19.03,3.61-26.1,5.94-6.24,16.2-10.65,36.53-11.75,55.54,18.72,20.34,48.67,39.14,57.32,45.66,19.06,14.37,42.45,2.6,42.45,2.6,1.03-.45,2.03-.93,3.01-1.43,12.43-7.74,21.97-17.95,26.43-29.4Z" />
      </g>
    </svg>
  </span>
</div>
```

***

### Message

**Description**  
Allows users to enter a message or request for an AI system to process and respond to.

**Classes:**  
- `.prs-message` - component: AI prompt
- `.prs-hint` - part: Hint subtext
- `.prs-message_hover` - state: Hover state
- `.prs-message_focus` - state: Focus state

**Example:**  
```html
<div class="prs-message" :class="{
  'prs-message_hover': state === 'hover',
  'prs-message_focus': state === 'focus',
}">
  <header x-show="withAttachments">
    <template x-for="i in 4" hidden>
      <div class="prs-attachment">
        <div class="prs-thumb"><svg width="24" height="24" role="img" fill="currentColor"><use href="/_assets/prs-icons.svg#content-type-blank-document"></use></svg></div>
        <div class="prs-meta">
          <div class="prs-name">file-name.pdf</div>
          <small class="prs-ext">application/pdf</small>
        </div>
        <button class="prs-close"><iconify-icon icon="mdi:close" noobserver></iconify-icon></button>
      </div>
    </template>
  </header>
  <label for="message-ai" class="sr-only">Message</label>
  <textarea x-model="message" id="massage-ai" placeholder="Type your message..." :disabled="state === 'disabled'"></textarea>
  <footer>
    <div>
      <button @click="withAttachments = !withAttachments" class="prs-btn prs-btn-tertiary prs-btn-square" :disabled="state === 'disabled'" aria-label="Attach"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" role="img" fill="currentColor"><use href="/_assets/prs-icons.svg#edit-add"></use></svg></button>
    </div>
    <div>
      <button class="prs-btn prs-btn-tertiary prs-btn-square" :disabled="state === 'disabled'" aria-label="Dictate"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" role="img" fill="currentColor"><use href="/_assets/prs-icons.svg#media-microphone"></use></svg></button>
      <button class="prs-btn prs-btn-primary prs-btn-square" :disabled="state === 'disabled' || !message.length" aria-label="Send"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" role="img" fill="currentColor"><use href="/_assets/prs-icons.svg#uncategorized-send"></use></svg></button>
    </div>
  </footer>
  <span class="prs-hint">AI can make mistakes. Don't type in personal information.</span>
</div>
```

***

### Pagination

**Description**  
Navigation aid that divides content into discrete pages, allowing users to navigate through large sets of data.

**Note:**  
Use **aria-current=&quot;true&quot;** on the active page button to set that as the current active page. This ensures the proper accessibility and rewards you with the proper styles.
Pay attention to the **aria-label** text for the current and non-current pages.
Also, note how the appropriate pagers get disabled when the first and last pages are active.

**Classes:**  
- `.prs-pagination` - component: Container
- `.prs-pagination-pager` - part: Page navigation
- `.prs-pagination-pager_disabled` - state: Page navigation disabled

**Example:**  
```html
<nav 
  class="prs-pagination" 
  role="navigation" 
  aria-label="Pagination"
  x-data="{
    totalPages: 5,
    currentPage: 1,

    goTo(page) {
      if (page < 1 || page > this.totalPages) return;
      this.currentPage = page;
    },
    prev() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    next() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    }
  }"
>
  <ul>
    <li class="prs-pagination-pager" :class="{ 'prs-pagination-pager_disabled': currentPage === 1 }">
      <a href="#" @click.prevent="prev()" aria-label="Previous Page">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#chevron-left" /></svg>
      </a>
    </li>
    <template x-for="page in totalPages" :key="page" hidden>
      <li>
        <a 
          href="#" 
          @click.prevent="goTo(page)"
          :aria-label="'Go to Page '+ page"
          :aria-current="currentPage === page ? 'true' : false"
          :class="{ 'active': currentPage === page }"
        >
          <span x-text="page"></span>
        </a>
      </li>
    </template>
    <li class="prs-pagination-pager" :class="{ 'prs-pagination-pager_disabled': currentPage === totalPages }">
      <a href="#" @click.prevent="next()" aria-label="Next Page">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" role="img"><use href="/_assets/prs-icons.svg#chevron-right" /></svg>
      </a>
    </li>
  </ul>
</nav>
```

***

### Progress

**Description**  
Visually represents the completion status of a task, process, or page load status.

**Classes:**  
- `.prs-progress` - component: Container
- `.prs-progress-radial` - component: Container
- `.prs-progress-label` - component: Container

**Example:**  
```html
<div x-show="!radial" class="prs-progress-label w-screen max-w-xs">
  <label x-show="label.length" for="progress-1" x-text="label"></label>
  <progress
    id="progress-1"
    :max="indeterminate ? false : 100"
    class="prs-progress"
    :class="{
      'prs-progress-secondary': variant === 'secondary',
      'prs-progress-accent': variant === 'accent',
      'prs-progress-info': variant === 'info',
      'prs-progress-success': variant === 'success',
      'prs-progress-warning': variant === 'warning',
      'prs-progress-danger': variant === 'danger',
      'prs-progress-neutral': variant === 'neutral',
    }"
    x-effect="indeterminate ? $el.removeAttribute('value') : $el.setAttribute('value', value)"
    x-text="value +'%'"
  ></progress>
  <label x-show="showValue && !indeterminate" for="progress-1" x-text="value +'%'"></label>
</div>

<div x-show="radial">
  <div
    x-text="value +'%'"
    class="prs-progress-radial"
    :class="{
      'prs-progress-secondary': variant === 'secondary',
      'prs-progress-accent': variant === 'accent',
      'prs-progress-info': variant === 'info',
      'prs-progress-success': variant === 'success',
      'prs-progress-warning': variant === 'warning',
      'prs-progress-danger': variant === 'danger',
      'prs-progress-neutral': variant === 'neutral',
    }"
    :style="'--value: '+ value" role="progressbar"
    :aria-valuenow="75"
  ></div>
</div>
```

***

### Radio

**Description**  
Form element that allows users to select one option from a group of choices.

**Classes:**  
- `.prs-radio` - component: For &lt;input&gt;
- `.prs-radio-label` - component: For &lt;label&gt;
- `.prs-radio_focus` - state: Manually apply visual focus

**Example:**  
```html
<label class="prs-radio-label max-w-sm">
  <input
    type="radio"
    name="radio-1"
    class="prs-radio"
    @click="checked ? checked = !checked : checked = $event.target.checked"
    @change="checked = $event.target.checked"
    :checked="checked"
    :class="{
      'prs-radio-lg': size === 'lg',
      'prs-radio-xl': size === 'xl',
      'prs-radio_focus': state === 'focus',
    }"
    :disabled="state === 'disabled'" />
  <span x-text="label ? label : 'Label'" class="prs-label-text"></span>
</label>
```

***

### Range

**Description**  
A range input allows users to select a value from a specified range.

**Classes:**  
- `.prs-range` - component: For &lt;input&gt; or &lt;label&gt;
- `.prs-range-secondary` - modifier: Secondary variant
- `.prs-range-accent` - modifier: Accent variant
- `.prs-range-info` - modifier: Blue variant
- `.prs-range-success` - modifier: Green variant
- `.prs-range-warning` - modifier: Yellow variant
- `.prs-range-danger` - modifier: Red variant
- `.prs-range_focus` - state: Manually apply visual focus
- `.prs-range_disabled` - state: Manually apply visual disabled

**Example:**  
```html
<div class="w-screen max-w-xs">
  <label class="form-control">
    <span x-show="label.length" class="prs-label">
      <span class="prs-label-text" x-text="label"></span>
    </span>
    <input
      type="range"
      min="1"
      max="100"
      x-model="value"
      step="1"
      class="prs-range"
      :class="{
        'prs-range-secondary': variant === 'secondary',
        'prs-range-accent': variant === 'accent',
        'prs-range-info': variant === 'info',
        'prs-range-success': variant === 'success',
        'prs-range-warning': variant === 'warning',
        'prs-range-danger': variant === 'danger',
        'prs-range_focus': state === 'focus',
      }"
      aria-label="Label"
      :disabled="state === 'disabled'" />
  </label>
  <span x-show="showValue" class="prs-label">
    <span class="prs-label-text"><span x-text="value"></span> <em class="text-xs"> / 100</em></span>
  </span>
</div>
```

***

### Select

**Description**  
Form element that allows users to to pick a value from a list of options.

**Note:**  
This is a modifier of **.prs-input**. Please use [input](../input/) properties and then stack **.prs-select** on top just for **select** tags.

**Classes:**  
- `.prs-select` - modifier: For use with select tag. This is meant to be used along side .prs-input

**Example:**  
```html
<div class="prs-form-control w-xl max-w-xs">
  <select
    id="preview-select"
    class="prs-input prs-select"
    :class="{
      'prs-input-ghost': variant === 'ghost',
      'prs-input_hover': state === 'hover',
      'prs-input_focus': state === 'focus',
    }"
    :disabled="state === 'disabled'"
  >
    <option selected disabled>Choose:</option>
    <template x-for="i in 3">
      <option x-text="'Option '+ i"></option>
    </template>
  </select>
</div>
```

***

### Separator

**Description**  
A visual way to separate sections of content or elements either horizontally or vertically.

**Classes:**  
- `.prs-separator` - component: For container
- `.prs-separator-vertical` - modifier: Flow vertically
- `.prs-separator-start` - modifier: Place object near the start
- `.prs-separator-end` - modifier: Place object near the end

**Example:**  
```html
<div class="w-screen p-6 max-w-sm" :class="orientation === 'vertical' && 'min-h-[calc(17rem)] flex justify-center gap-4'">
  <div
    class="prs-separator"
    :class="{
      'prs-separator-vertical': orientation === 'vertical',
      'prs-separator-start': position === 'start',
      'prs-separator-end': position === 'end',
    }"
    x-text="text"
  ></div>
</div>
```

***

### Skeleton

**Description**  
A faux UI to indicate the loading state of a component or UI Block.

**Classes:**  
- `.prs-skeleton` - component: For container
- `--skel-width` - token: Width
- `--skel-height` - token: Height
- `--skel-radius` - token: Corner/border radius
- `--skel-bg` - token: Background color (converted to 90% transparent)
- `--skel-fg` - token: Gradient base color (converted to 30% transparent)

**Example:**  
```html
<div x-show="!real" class="p-4 flex items-center justify-center absolute inset-px rounded-[calc(var(--radius-box)-1px)]">
  <div class="prs-skeleton" :style="{
    '--skel-width': (width !== '0') ? width +'rem' : '100%',
    '--skel-height': (height !== '0') ? height +'rem' : '1rem',
    '--skel-radius': radius +'px',
    '--skel-bg': background !== '' ? background : 'currentColor',
    '--skel-fg': foreground,
  }"></div>
</div>
<div x-show="real" class="p-4 w-screen max-w-xs bg-white flex items-center gap-2 rounded-box">
  <div class="shrink-0">
    <div class="prs-skeleton" style="--skel-width: 3rem; --skel-height: 3rem; --skel-radius: 9999px;"></div>
  </div>
  <div class="grow space-y-2">
    <div class="prs-skeleton" style="--skel-width: 75%;"></div>
    <div class="prs-skeleton"></div>
  </div>
</div>
```

***

### Tab

**Description**  
Navigation aid that allows users to switch between different sections or views within the same page.

**For best accessibility:**  
Use **button** tag for tab. Also make sure to use **tabindex=&quot;-1&quot;** on inactive tabs and **tabindex=&quot;0&quot;** on the active tab so the user can ONLY focus the active tab. You are also responsible for implementing keyboard commands to move the focused tab (arrow left/right, pgup/dn, home/end). The tab and associated tabpanel should activate/follow the active tab. Please use [MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/tab_role#keyboard_interactions) as a reference for full accessibility requirements.

**Classes:**  
- `.prs-tabs` - component: Container
- `.prs-tabs-center` - modifier: Justify center
- `.prs-tab` - part: For &lt;button&gt;
- `.prs-tab_active` - state: Currently active

**Example:**  
```html
<div class="border-b border-(--prs-c-gray-300) w-screen max-w-sm [&_button]:-mb-px">
  <div
    role="tablist"
    class="prs-tabs"
    :class="{
      'prs-tabs-center': center
    }"
  >
    <button
      @mousedown.prevent
      @click.prevent
      id="tab-1"
      :tabindex="active ? 0 : -1"
      :aria-selected="active"
      :class="{
        'prs-tab_hover': state === 'hover',
        'prs-tab_focus': state === 'focus',
        'prs-tab_active': active, 
      }
      "
      class="prs-tab"
      role="tab"
      :disabled="state === 'disabled' ? true : false"
    >
      <span>Tab</span>
      <span x-show="withBadge" class="prs-badge">5</span>
    </button>
  </div>
</div>
```

***

### Table

**Description**  
Element that displays tabular data in a structured format of rows and columns.

**Classes:**  
- `.prs-table-container` - component: Container
- `.prs-table` - component: For &lt;table&gt;
- `.prs-table-fixed` - modifier: Equal column widths
- `.prs-table-bordered` - modifier: Add divider lines
- `.prs-table-striped` - modifier: Even/odd highlight
- `.prs-table-compact` - modifier: Less padding
- `.prs-table-pin-rows` - modifier: Sticky &lt;thead&gt; and &lt;tfoot&gt;
- `.prs-table-pin-cols` - modifier: Sticky &lt;th&gt; columns
- `.prs-cell-name` - part: Name/email
- `.prs-cell-stacked` - part: Stacked content
- `.prs-cell-end` - part: Justify end/right
- `.prs-cell-actions` - part: Header cell actions container
- `.prs-cell-info` - part: Info tooltip container
- `.prs-cell-sort` - part: Sorting container

**Example:**  
```html
<div class="prs-table-container w-screen max-w-lg max-h-[16rem]">
  <table class="prs-table" :class="{
    'prs-table-fixed': fixed,
    'prs-table-bordered': bordered,
    'prs-table-striped': striped,
    'prs-table-compact': compact,
    'prs-table-pin-rows': pinRows,
    'prs-table-pin-cols': pinCols,
  }">
    <thead>
      <tr>
        <th></th>
        <th class="w-fit" :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span :class="((pinCols || pinRows) && !fixed) && 'whitespace-nowrap'">Header</span>
            <strong x-show="subLabel" class="whitespace-nowrap" x-text="'Sub label'"></strong>
          </div>
        </th>
        <th class="w-fit" :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span :class="((pinCols || pinRows) && !fixed) && 'whitespace-nowrap'" x-text="pinRows ? 'Header with longer label' : 'Header'"></span>
            <strong x-show="subLabel" class="whitespace-nowrap" x-text="'Sub label'"></strong>
          </div>
        </th>
        <th class="w-fit" :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span :class="((pinCols || pinRows) && !fixed) && 'whitespace-nowrap'">Header</span>
            <strong x-show="subLabel" class="whitespace-nowrap" x-text="'Sub label'"></strong>
          </div>
        </th>
        <th class="w-fit" :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span :class="((pinCols || pinRows) && !fixed) && 'whitespace-nowrap'">Header</span>
            <strong x-show="subLabel" class="whitespace-nowrap" x-text="'Sub label'"></strong>
          </div>
        </th>
        <th class="w-fit" :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span :class="((pinCols || pinRows) && !fixed) && 'whitespace-nowrap'">Header</span>
            <strong x-show="subLabel" class="whitespace-nowrap" x-text="'Sub label'"></strong>
          </div>
        </th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th class="w-px text-xs font-bold">#.</th>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <th class="w-px text-xs font-bold">#.</th>
      </tr>
      <tr>
        <th class="w-px text-xs font-bold">#.</th>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <th class="w-px text-xs font-bold">#.</th>
      </tr>
      <tr>
        <th class="w-px text-xs font-bold">#.</th>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <th class="w-px text-xs font-bold">#.</th>
      </tr>
      <tr>
        <th class="w-px text-xs font-bold">#.</th>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <th class="w-px text-xs font-bold">#.</th>
      </tr>
      <tr>
        <th class="w-px text-xs font-bold">#.</th>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <td :class="{
          'prs-cell-end': end,
        }">
          <div class="prs-cell-stacked">
            <span>Cell</span>
            <em class="whitespace-nowrap" x-show="subData">Some data</em>
          </div>
        </td>
        <th class="w-px text-xs font-bold">#.</th>
      </tr>
    </tbody>
  </table>
</div>
<p class="kbd kbd-sm font-semibold absolute top-1 left-1 pointer-events-none select-none">Scrollable on x/y axis</p>
```

***

### Textarea

**Description**  
Form element that allows users to input and edit text or data into a website page.

**Note:**  
This is a modifier of **.prs-input**. Please use [input](../input/) properties and then stack **.prs-textarea** on top just for **textarea** tags.

**Classes:**  
- `.prs-textarea` - component: For &lt;textarea&gt;

**Example:**  
```html
<div class="prs-form-control w-screen max-w-xs">
  <textarea
    id="preview-textarea"
    x-model="value"
    class="prs-input prs-textarea"
    :class="{
      'prs-input-ghost': variant === 'ghost',
      'prs-input_focus': state === 'focus',
    }"
    :placeholder="placeholder"
    :disabled="state === 'disabled'"
  ></textarea>
</div>
```

***

### Toggle

**Description**  
Form element that allows users to switch between two states, such as on and off.

**For best accessibility:**  
Use **role=&quot;switch&quot;** on the **input** so it represents **on**/**off** instead of _checked/unchecked_. Make sure to ALWAYS use a **label** wrapped around the toggle to ensure a more accessible target click area.

**Classes:**  
- `.prs-toggle` - component: For &lt;input&gt;
- `.prs-toggle-label` - component: For &lt;label&gt;
- `.prs-toggle-secondary` - modifier: Secondary color variant
- `.prs-toggle-accent` - modifier: Accent color variant
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
<div
  x-init="
    $watch('checked', value => {
      indeterminate = false;
    });
    $watch('indeterminate', value => {
      $nextTick(() => {
        $refs.prsToggle.indeterminate = value;
        $refs.prsToggleIcon.indeterminate = value;
      });
    });
  "
  class="w-fit max-w-sm"
> <!-- <- this is just for demo purposes -->
  <label class="prs-toggle-label">
    <span x-show="!trailingLabel" class="prs-label-text" x-text="label"></span>
    <input
      type="checkbox"
      x-show="!icon"
      x-model="checked"
      x-ref="prsToggle"
      x-init="$el.indeterminate = indeterminate"
      :class="{
        'prs-toggle-sm': small,
        ['prs-toggle-'+ variant]: variant !== 'default',
        'prs-toggle_focus': state === 'focus',
      }"
      class="prs-toggle"
      role="switch"
      :disabled="state === 'disabled'"
    />
    <span
      x-show="icon"
      :class="{
        'prs-toggle-sm': small,
        ['prs-toggle-'+ variant]: variant !== 'default',
        'prs-toggle_focus': state === 'focus',
      }"
      class="prs-toggle"
    >
      <input type="checkbox" x-model="checked" x-ref="prsToggleIcon" x-init="$el.indeterminate = indeterminate" :aria-label="label" role="switch" :disabled="state === 'disabled'" />
      <span><iconify-icon icon="mdi:close" noobserver></iconify-icon></span>
      <span><iconify-icon icon="mdi:check" noobserver></iconify-icon></span>
    </span>
    <span x-show="trailingLabel" class="prs-label-text" x-text="label"></span>
  </label>
</div>
```

***

### Tooltip

**Description**  
Small pop-up element that provides additional information when users hover or focus on an element.

**Note:**  
This is a pure CSS alternative to something like [Tippy.js](https://atomiks.github.io/tippyjs/). We HIGHLY recommend you use a proper positioning library so the tooltip never appears outside the viewport. Sadly, vanilla CSS cannot do this... _YET!_

**Classes:**  
- `.prs-tooltip` - component: For actionable item, use [data-tip=&quot;BLAH&quot;] to house the tooltip content
- `.prs-tooltip-content` - component: Optional content container, use if you need to embed HTML

**Example:**  
```html
<div
  class="prs-tooltip"
  :class="{
    'prs-tooltip-open': open,
    'prs-tooltip-bottom': position === 'bottom',
    'prs-tooltip-left': position === 'left',
    'prs-tooltip-right': position === 'right',
  }"
  :data-tip="text ? text : 'Tooltip'"
>
  <div x-show="embed" class="prs-tooltip-content">
    <div class="animate-bounce text-(--prs-c-warning) -rotate-6 text-base font-black">Fancy</div>
  </div>
  <button class="prs-btn prs-btn-secondary" :disabled="open">
    <span x-text="position" class="capitalize"></span>
  </button>
</div>
<p x-show="!open" x-transition class="kbd kbd-sm font-semibold absolute top-1 left-1 pointer-events-none select-none">Hover / Focus</p>
```

