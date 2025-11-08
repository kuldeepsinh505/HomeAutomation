# SmartHome Pro - Design Guidelines

## Design Approach

**Selected Framework**: Hybrid approach drawing from **Google Home** and **Apple Home** design patterns - combining Material Design's clarity for data-dense interfaces with iOS Home's intuitive touch controls. This utility-focused application prioritizes quick access, real-time feedback, and fail-safe emergency controls.

## Core Design Principles

1. **Instant Recognition** - Device status must be understood at a glance
2. **Touch-First Interaction** - All controls optimized for thumb reach on mobile
3. **Safety-Critical Design** - Emergency "Turn Off All" button always prominent and unmistakable
4. **Real-time Feedback** - Visual confirmation for every action within 100ms

## Typography System

**Font Families**:
- Primary: Inter (via Google Fonts)
- Monospace: JetBrains Mono (for device IDs, technical data)

**Hierarchy**:
- Hero/Dashboard Title: Inter Bold, text-3xl (30px)
- Section Headers: Inter Bold, text-xl (20px)
- Room/Device Names: Inter Semibold, text-lg (18px)
- Body/Controls: Inter Regular, text-base (16px)
- Metadata/Timestamps: Inter Regular, text-sm (14px), opacity-70
- Technical Data: JetBrains Mono Regular, text-xs (12px)

## Layout System

**Spacing Units**: Use Tailwind units of **2, 3, 4, 6, 8, 12** for consistent rhythm
- Component padding: p-4, p-6
- Section spacing: gap-4, gap-6
- Card margins: m-2, m-4
- Icon spacing: space-x-3, space-y-2

**Grid System**:
- Dashboard room cards: grid-cols-2 (mobile), grid-cols-3 (tablet)
- Device controls: Single column focus on mobile
- Settings lists: Full-width single column
- Bottom nav: 5 equal-width columns

**Container Constraints**:
- Max width: max-w-7xl for content
- Padding: px-4 on mobile, px-6 on tablet
- Safe areas: pb-24 to account for bottom navigation

## Component Library

### Navigation
**Bottom Tab Bar**:
- Fixed position with backdrop blur
- Height: h-16
- Icons: 24px with labels below (text-xs)
- Active state: Primary color with subtle scale transform

**Headers**:
- Height: h-14
- Back buttons: Chevron left with text
- Action buttons: Top right, icon-only

### Cards & Containers
**Room Cards**:
- Rounded corners: rounded-2xl
- Padding: p-6
- Shadow: shadow-lg with subtle border
- Device count badge: Absolute positioned top-right

**Device Cards**:
- Compact height: min-h-20
- Horizontal layout: Icon left, controls right
- Quick toggle switch prominently placed
- Status indicator: Colored dot (8px) top-right

**Control Panels**:
- Full-width on device detail screens
- Large touch targets: min-h-12 for sliders
- Rounded: rounded-xl
- Generous padding: p-8

### Buttons & Controls
**Emergency "Turn Off All"**:
- **Critical Design**: Full-width, rounded-full, h-14
- Red background with pulsing animation
- Bold white text: "Turn Off All Devices"
- Positioned prominently on dashboard (below weather widget)
- Requires confirmation modal

**Primary Actions**:
- Height: h-12, rounded-lg
- Padding: px-6
- Font: Inter Semibold

**Toggle Switches**:
- Large hit area: 56x32px minimum
- Smooth spring animation on state change
- Active color: Electric Green
- Inactive: Slate Gray with 50% opacity

**Sliders** (Brightness/Temperature):
- Track height: h-2
- Thumb size: 24px circle
- Active track: Gradient based on device type
- Value label follows thumb

**Floating Action Button**:
- Size: 56x56px circle
- Bottom-right: bottom-20 right-4
- Shadow: shadow-2xl with elevation
- Icon: 24px centered

### Status Indicators
**Device Status Dots**:
- Size: w-3 h-3 rounded-full
- Colors: Green (online), Red (offline), Amber (warning), Gray (inactive)
- Pulse animation for state changes

**Connection Quality**:
- WiFi bars icon with opacity levels
- Text indicator: "Excellent", "Good", "Poor", "Offline"

### Data Visualization
**Energy Monitoring Charts**:
- Minimal line charts with gradient fills
- Grid lines: subtle (opacity-10)
- Height: h-48 for overview cards
- Interactive tooltips on hover/tap

**Usage Statistics**:
- Horizontal bar charts for comparisons
- Percentage indicators with icons
- Color coding: Green (low), Amber (moderate), Red (high)

## Screen-Specific Patterns

### Dashboard
- Weather widget: Horizontal card with icon, temp, location
- Room grid: 2 columns, gap-4
- Emergency button: Centered, full-width, mb-6
- Recent activity: List view with timestamps (text-xs)

### Device Control
- Hero area: Large icon (64px) + device name
- Control section: Centered, max-w-md
- Settings accordion: Collapsible sections with chevrons
- Action buttons: Fixed bottom with backdrop blur

### Automation Scenes
- Scene cards: Image background with overlay gradient
- Quick activate: Large circular button overlay
- Grid: 2 columns for scene gallery
- Preview states: Semi-transparent device icons

### Room Details
- Header: Room name + device count badge
- "Turn Off Room" button: Secondary style, mb-4
- Device grid: Compact cards, 1 column
- Add device: Dashed border card at end

## Animations

**Minimal, Purposeful Animations**:
- State changes: 200ms ease-in-out
- Toggle switches: Spring animation (200ms)
- Card entry: Stagger fade-in (100ms delay per item)
- Emergency button: Subtle pulse (2s infinite)
- Pull-to-refresh: Custom animation with loading indicator
- **No decorative scroll effects or parallax**

## Accessibility

- All touch targets: Minimum 44x44px
- Color contrast: WCAG AA minimum (4.5:1 for text)
- Focus indicators: 2px outline with offset
- Status communicated via text + color + icons
- Voice-over labels for all interactive elements
- Haptic feedback for critical actions (emergency button)

## Images

**No hero images needed** - This is a utility app focused on controls and real-time data. Device imagery consists of:
- **Device Icons**: Use icon library placeholders (thermostat, lightbulb, lock, camera icons)
- **Scene Thumbnails**: Generic scene icons (moon for sleep, TV for movie night, home for arrival)
- **Empty States**: Simple illustrations for "No devices" or "No automations"
- **Profile Avatars**: User-uploaded or default avatar icons

All imagery should be functional, not decorative, maintaining the utility-focused design approach.