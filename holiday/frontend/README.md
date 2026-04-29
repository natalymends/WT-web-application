# WT Web Application — Client

This folder contains the frontend for the Holiday Calendar project. It's a React application scaffolded with Vite, providing authentication, an interactive calendar UI, event creation (including recurrence), and integration with the backend API hosted in the `holiday/backend` folder.

---

## Project Structure

```
client/
├── public/
│   └── index.html
├── src/
│   ├── api/
│   │   ├── axiosInstance.js       # Axios instance with base URL + interceptors
│   │   ├── authApi.js             # Login / register / session API calls
│   │   └── eventsApi.js           # Event CRUD and recurrence API calls
│   ├── assets/                    # Images and static assets
│   ├── components/
│   │   ├── auth/                  # LoginForm.jsx, SignupForm.jsx
│   │   ├── calendar/              # CalendarHeader.jsx, MonthView.jsx, WeekView.jsx, DayView.jsx
│   │   ├── events/                # EventForm.jsx, EventModal.jsx, RecurrenceSelector.jsx
│   │   └── ui/                    # Button.jsx, Modal.jsx, Navbar.jsx, Spinner.jsx
│   ├── context/                   # AuthContext.jsx, CalendarContext.jsx
│   ├── hooks/                     # useAuth.js, useCalendar.js, useEvents.js, useRecurrence.js, useDragAndDrop.js
│   ├── pages/                     # CalendarPage.jsx, LoginPage.jsx, SignupPage.jsx, ProfilePage.jsx
│   ├── routes/                    # AppRoutes.jsx
│   ├── utils/                     # dateUtils.js, recurrenceUtils.js, env.js
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── package.json
├── postcss.config.js
└── tailwind.config.js
```

---

## Implementations

1. App entry & routing

- `src/main.jsx` and `src/App.jsx` bootstrap the React app and register global providers.
- `src/routes/AppRoutes.jsx` defines public and protected routes using `AuthContext`.

2. Authentication

- `components/auth/LoginForm.jsx` and `SignupForm.jsx` perform client-side validation and call `src/api/authApi.js` endpoints (`/login`, `/register`, `/logout`, `/session`).
- `useAuth.js` and `AuthContext.jsx` manage authenticated user state and expose `login`, `logout`, and `register` helpers.
- `axiosInstance.js` configures the base URL and handles errors (e.g., 401 responses) centrally.

3. Calendar UI

- `pages/CalendarPage.jsx` composes the main calendar view and related overlays.
- `components/calendar/MonthView.jsx`, `WeekView.jsx`, and `DayView.jsx` render different calendar granularities, relying on `utils/dateUtils.js` for date calculations.
- `components/calendar/CalendarHeader.jsx` provides UI for view switching and date navigation.

4. Events & recurrence

- `components/events/EventForm.jsx` enables creating and editing events, including recurrence options.
- `components/events/RecurrenceSelector.jsx` exposes recurrence rule selection and normalisation via `utils/recurrenceUtils.js`.
- `useEvents.js` coordinates fetching, caching, and optimistic updates for event operations.

5. State & context

- `AuthContext.jsx` holds authentication state and session checks.
- `CalendarContext.jsx` stores the selected date, current view (month/week/day), and UI modal states.
- Hooks (`useCalendar`, `useEvents`, `useRecurrence`) encapsulate component logic for reuse and testing.

6. Drag-and-drop

- `useDragAndDrop.js` enables dragging events between days to reschedule. Views integrate this hook for interactive behaviour.

7. API integration

- `src/api/axiosInstance.js` centralises API configuration (base URL, credentials, interceptors).
- `authApi.js` and `eventsApi.js` wrap HTTP calls used by hooks and components.

8. UI primitives & styling

- Reusable UI components live in `components/ui/` and are used across the app for consistent styling and accessibility.
- Tailwind CSS is used for styling and configured via `tailwind.config.js` and `postcss.config.js`.

9. Utilities

- `utils/dateUtils.js` — helpers for formatting dates and computing calendar ranges.
- `utils/recurrenceUtils.js` — parse/serialize recurrence rules for UI and backend interchange.
- `utils/env.js` — runtime configuration helpers (API base URL from environment).

10. Testing

- Components and hooks are structured for unit testing; add test files and a test runner if you want test coverage for the client.

---

## How frontend maps to backend

- Authentication flows use the backend auth routes for session management and cookie-based persistence.
- Holidays and event-related operations use the backend endpoints for listing, creating, updating, and deleting resources.
- Favourite and suggestion UI features call the related backend endpoints where applicable.

---

## Division of Labour (client)

- All work evenly divided

---

## References

- Vite: https://vitejs.dev/
- React: https://reactjs.org/
- Tailwind CSS: https://tailwindcss.com/

