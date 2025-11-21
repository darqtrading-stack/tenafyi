# AI Tenant Qualification Chatbot - Design Guidelines

## Design Approach

**Selected Approach:** Messaging Platform Reference (WhatsApp/Messenger) + Fintech Dashboard Hybrid

Drawing from WhatsApp's conversational intimacy and Stripe/Plaid's trust-building financial interfaces. The chatbot should feel like a professional advisor having a natural conversation while displaying structured data clearly.

---

## Layout System

**Spacing Primitives:** Use Tailwind units of 2, 4, 6, and 8 for consistency (p-2, p-4, m-6, gap-8)

**Container Structure:**
- Chat container: max-w-3xl centered with full viewport height
- Message bubbles: max-w-md for readability
- Property cards: max-w-lg within chat flow
- Income displays: max-w-sm for focused data

**Viewport Strategy:**
- Full-height chat interface (h-screen with flex column)
- Fixed header (agency branding + status)
- Scrollable message area (flex-1 overflow-y-auto)
- Fixed input area at bottom

---

## Typography

**Font Family:** Inter or DM Sans from Google Fonts (professional, highly legible)

**Hierarchy:**
- Agency name/header: text-lg font-semibold
- Bot messages: text-base font-normal
- User messages: text-base font-normal  
- Property titles: text-lg font-semibold
- Financial figures: text-2xl font-bold (tabular-nums)
- Labels/metadata: text-sm font-medium
- Helper text: text-xs text-opacity-70

---

## Component Library

### Header Component
- Agency logo/name (left)
- Online status indicator with pulse animation
- Info icon for help (right)
- Subtle border-bottom for separation

### Message Bubbles
**Bot Messages (left-aligned):**
- Rounded corners: rounded-2xl rounded-tl-md (tail effect)
- Padding: p-4
- Max width prevents text sprawl
- Avatar circle (w-8 h-8) with agency icon/initials

**User Messages (right-aligned):**
- Rounded corners: rounded-2xl rounded-tr-md
- Padding: p-4
- Right-aligned with ml-auto

**Typing Indicator:**
- Three animated dots (scale pulse)
- Same styling as bot bubble

### Property Card Component (Inline in Chat)
**Structure:**
- Full-width within max-w-lg constraint
- Image: aspect-video with object-cover, rounded-t-xl
- Content padding: p-5
- Property title: prominent, font-semibold
- Location: with map pin icon
- Key details grid: 2 columns (Bedrooms, Rent, Available)
- "View Details" link with arrow icon

### Income Calculation Display
**Progressive Disclosure:**
- Initial summary card showing "Required Income: £XX,XXX"
- Expandable breakdown section:
  - Monthly rent multiplier shown
  - Income requirement formula
  - Simple bar visualization showing user's income vs requirement
  - Pass/Warning/Fail status with appropriate iconography

**Calculator Display:**
- Input-style presentation even though pre-filled
- Label + large number display
- Checkmark/warning icons inline
- Clear visual separation between sections (border-t with spacing)

### Input Area
- Sticky bottom with backdrop-blur for elevation
- Text input: rounded-full with generous padding (py-3 px-5)
- Send button: circular, icon-only (paper plane)
- Optional quick reply chips above input (rounded-full pills)
- Disabled state when bot is typing

### Quick Reply Buttons
- Pill-shaped (rounded-full)
- Inline-flex with gap-2 spacing
- Wrap on multiple rows
- Subtle border, no fill until hover
- Icon + text combinations where helpful

---

## Images

### Header/Branding Area
**Agency Logo:** Rectangular logo (120x40px recommended) in header. Should be clean, professional wordmark or combined logo-mark.

### Property Cards
**Property Photos:** High-quality exterior/interior shots, aspect-video ratio (16:9). Each property card displays one hero image. Images should show:
- Well-lit property exteriors
- Modern, clean interiors
- Professional real estate photography style
- Consistent aspect ratio across all cards

**Placement:** Images appear inline within the chat flow as part of property card components when the bot presents available properties.

### No Large Hero Image
This is a functional chat interface, not a marketing page. No hero section needed - users dive directly into conversation.

---

## Animation Strategy

**Minimal, Purposeful Motion:**
- Message bubbles: subtle slide-up on entry (translate-y-2 to 0)
- Typing indicator: gentle dot pulse
- Status pulse: soft 2s cycle on "online" indicator
- Quick replies: subtle scale on tap
- NO scroll animations, parallax, or decorative motion

---

## Accessibility Implementation

**Consistent Patterns:**
- All interactive elements: min-height of 44px (touch target)
- Focus states: 2px ring with offset
- ARIA labels on icon-only buttons
- Semantic HTML: `<main>` for chat area, `<form>` for input
- Contrast ratios meet WCAG AA minimum
- Screen reader announcements for new messages (aria-live="polite")

---

## Professional Trust Elements

**Visual Signals:**
- Agency logo prominently placed
- Professional typography (no playful fonts)
- Structured data presentation in cards
- Clear calculation transparency
- Progress indicators showing qualification steps
- Secure/encrypted messaging indicator in header

**Information Architecture:**
1. Welcome message with bot introduction
2. Property preference questions (location, budget, bedrooms)
3. Property suggestions with inline cards
4. Financial qualification questions
5. Income calculation display with clear breakdown
6. Next steps or scheduling

This creates a professional yet approachable experience that balances conversational ease with the gravity of rental qualification decisions.