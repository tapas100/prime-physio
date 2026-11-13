# Prime Physio — product architecture

## Product principles
- One product with three workspaces: Patient, Physiotherapist, Admin.
- A single shared component library and token system.
- Appointment is the central workflow entity. Role-specific permissions govern visibility and actions.
- Physiotherapist scope is deliberately limited to appointment management and one session summary per appointment. No goals, exercise plans, or exercise library in this scope.

## Page inventory

### Patient
1. Patient home — next appointment, status, recent visits, profile shortcut.
2. My appointments — upcoming/past appointments, status filters, loading/empty/error states.
3. Appointment details — date/time, location, assigned physiotherapist, status, instructions, allowed reschedule/cancel actions.
4. Visit history — completed sessions and available summaries.
5. My profile — personal/contact details and account preferences.

### Physiotherapist
1. Physiotherapist home — today's schedule, next patient, workload snapshot.
2. Appointment worklist — day/list view, patient/status filters, start/resume actions.
3. Appointment details — patient identity/contact, date/time, status, relevant context.
4. Active session — focused patient/appointment context and session state.
5. Session summary — a single structured record of what was performed, observations/response, notes, performed-by attribution and completion time; save and complete. This is not an exercise or goals screen.

### Admin
1. Admin dashboard — appointments today, patient/physiotherapist counts, operational status.
2. Patient management — searchable/filterable list, add/edit/deactivate.
3. Patient details — demographics, contact, appointment history, account status.
4. Physiotherapist management — searchable/filterable staff list, add/edit/deactivate.
5. Physiotherapist details — profile, professional details, availability/status. Appointment browsing is intentionally not embedded here.
6. Appointment management — searchable/filterable list, create/reschedule/cancel/update status.
7. Appointment details — patient, physiotherapist, date/time, status, performed by and session summary.

## Reusable component inventory

### App shell and navigation
AppShell, RoleSwitcher (demo/dev only), Sidebar, MobileTabBar, TopBar, PageHeader, Breadcrumbs, NavItem, UserMenu, NotificationButton.

### Data display
StatCard, StatusBadge, Avatar, AvatarGroup, EmptyState, Skeleton, InlineAlert, DataTable, TableToolbar, SearchField, FilterChips, Pagination, AppointmentCard, AppointmentRow, PatientIdentity, PhysiotherapistIdentity, DetailList, Timeline.

### Forms and actions
Button (primary/secondary/tertiary/destructive), IconButton, TextField, TextArea, SelectField, DateTimeField, FormField, Modal, ConfirmDialog, Drawer, DropdownMenu, Tabs, SegmentedControl, SessionSummaryForm, FormSection, SaveBar.

### Feedback and access
Toast, Tooltip, LoadingSpinner, ErrorState, PermissionGate, ErrorBoundary.

## Theme palette — Prime, Apple-inspired
An original visual language informed by Apple's clarity, typography hierarchy, restrained chrome, generous spacing, and native-feeling controls. It is not a reproduction of Apple's proprietary UI.

| Token | Light | Dark | Purpose |
|---|---|---|---|
| Accent | #176B5B | #70C7B2 | Primary actions/active state |
| Accent strong | #105448 | #8AD8C5 | Hover/pressed state |
| Accent soft | #E6F3EF | #183A34 | Selected surfaces |
| Canvas | #F5F6F8 | #101214 | App background |
| Surface | #FFFFFF | #1A1D20 | Cards/panels |
| Surface secondary | #F0F2F4 | #24282C | Grouped surfaces |
| Text primary | #171A1C | #F4F6F7 | Main copy |
| Text secondary | #687078 | #AAB2B9 | Supporting copy |
| Border | #E3E7EA | #30363B | Separators |
| Success | #16845B | #56C995 | Completed/confirmed |
| Warning | #B7791F | #E7B75E | Pending/attention |
| Danger | #C44747 | #F08080 | Cancelled/destructive |
| Info | #3174C7 | #7DADEB | Informational |

### Interaction and layout rules
- System font stack, preferring SF Pro on Apple platforms; 14–16px body; distinct page-title hierarchy.
- 8px spacing scale; controls 12px radius; cards 18–22px radius; subtle borders and restrained shadows.
- 44px minimum touch targets; keyboard-visible focus; explicit loading, disabled, error and empty states.
- Teal reserved for primary actions and selected states; status uses both text and color.
- Motion 150–220ms ease-out; respect prefers-reduced-motion.
- Responsive: desktop sidebar, compact tablet layout, mobile navigation.
- Token-based light/dark themes; avoid hardcoded per-component colors.

## Folder conventions
- src/app — bootstrap, route map, providers
- src/layouts — role-aware application shells
- src/components/ui — generic visual primitives
- src/components/domain — appointment/patient/staff components
- src/features/{role}/{feature} — role-owned screens and workflows
- src/design-system — tokens, theme, global styles
- src/lib — utilities and mock data
- src/types — shared domain types
- docs — architecture and product decisions
