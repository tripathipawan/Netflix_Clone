# 🎬 Netflix Clone

A pixel-faithful Netflix UI clone built with **React**, **Firebase**, and **CSS** — featuring a fully functional authentication system (sign up, sign in, sign out), persistent login sessions via `react-firebase-hooks`, protected routing, toast notifications for auth feedback, and a multi-page layout that faithfully replicates Netflix's visual design language including the hero banner, category rows, and hover card effects.

---

## 📌 Overview

This project recreates the Netflix frontend experience — from the landing and authentication screens through to the authenticated home browsing interface — using React for the UI, Firebase Authentication for account management, and `react-firebase-hooks` for real-time auth state binding to React's render cycle.

Every route is protected: unauthenticated users are redirected to the sign-in page automatically, and signed-in users are sent directly to the home page. Firebase handles all session persistence — users stay logged in across browser refreshes without any custom backend.

---

## ✨ Features

- **Firebase Email / Password Authentication** — Complete auth flow built on Firebase Auth's `createUserWithEmailAndPassword` and `signInWithEmailAndPassword`. Firebase handles credential validation, password hashing, and secure JWT token management entirely on its infrastructure.
- **Persistent Login Sessions** — `react-firebase-hooks`'s `useAuthState` hook subscribes to Firebase Auth's real-time auth state observer. When a user signs in, the session persists across browser refreshes automatically — Firebase stores the JWT in `localStorage` and re-hydrates it on every page load.
- **Protected Route Architecture** — React Router DOM v7 routes are guarded by auth state checks. Authenticated users accessing `/signin` or `/signup` are redirected to `/home`. Unauthenticated users accessing `/home` are redirected to `/signin` — both enforced via React Router's `<Navigate>` component inside `App.jsx`.
- **Toast Notifications for All Auth Events** — `react-toastify` displays non-intrusive feedback toasts for every authentication action — successful account creation, sign-in confirmation, auth errors (wrong password, user not found, email already in use), and sign-out confirmation.
- **Sign Up Page** — Registration form with email and password fields. Firebase creates the account on submission; the user is automatically signed in and redirected to the home page. Duplicate email errors are caught and surfaced as error toasts.
- **Sign In Page** — Netflix-styled login card — dark background, centered form, branded red action button. Firebase validates credentials; all error cases (wrong password, no account) are caught and shown to the user via toast messages.
- **Netflix-Style Home Page** — The authenticated home replicates Netflix's browsing UI: a fixed top navbar with logo, category links, user icon and sign-out control; a full-width hero banner section; and multiple horizontally scrollable movie/show rows organized by category.
- **Hero Banner** — A large full-bleed background image section with a featured title, description text, and "Play" and "More Info" action buttons — styled to match Netflix's hero section with gradient overlay for text readability.
- **Movie / Show Row Sections** — Horizontally scrollable rows of movie and show thumbnail cards categorized by genre. Cards scale up on hover with a smooth CSS `transform: scale()` transition, replicating Netflix's card interaction exactly.
- **Fixed Navbar** — Persistent top navigation bar with the Netflix logo, browse category links, and a profile icon with logout action — sticking to the top as the user scrolls through content rows.
- **Sign Out** — Calls Firebase Auth's `signOut()` method, clears the active session, shows a success toast, and redirects to the sign-in page via React Router.
- **Fully Responsive Design** — CSS media queries adapt the navbar, hero section, and movie row card sizes correctly across mobile, tablet, and desktop viewports.
- **Vite Build Tooling** — Fast development server with instant HMR via Vite and `@vitejs/plugin-react`.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| React 18 | Component-based UI and SPA architecture |
| JavaScript (ES6+) | Component logic, async Firebase auth calls, event handling |
| Vite | Development server, HMR, and production bundling |
| Firebase Authentication | Email/password sign up, sign in, session persistence, sign out |
| `react-firebase-hooks` | `useAuthState` hook — real-time Firebase auth state in React |
| React Router DOM v7 | Client-side routing with auth-based protected route redirects |
| react-toastify | Toast notifications for all auth events and error messages |
| CSS3 | All component styling — Netflix visual design, hover effects, responsive layout |

---

## 📁 Project Structure

```
Netflix_Clone/
├── public/                          # Static assets (favicon, logo images)
├── src/
│   ├── components/                  # Reusable UI components
│   │   ├── Navbar/
│   │   │   ├── Navbar.jsx           # Fixed top nav — Netflix logo, links, user icon, sign-out button
│   │   │   └── Navbar.css           # Navbar styles — dark background, flex layout, scroll behavior
│   │   ├── Banner/
│   │   │   ├── Banner.jsx           # Hero section — background image, title, description, action buttons
│   │   │   └── Banner.css           # Full-width background, gradient overlay, Play/Info button styles
│   │   ├── Row/
│   │   │   ├── Row.jsx              # Horizontally scrollable category row of movie/show cards
│   │   │   └── Row.css              # Overflow-x scroll, card sizing, scrollbar hiding
│   │   └── MovieCard/
│   │       ├── MovieCard.jsx        # Individual thumbnail card — poster image, hover scale effect
│   │       └── MovieCard.css        # Card hover animation — CSS transform scale with transition
│   ├── pages/                       # Route-level page components
│   │   ├── Home/
│   │   │   ├── Home.jsx             # Authenticated home — Navbar, Banner, all Row category sections
│   │   │   └── Home.css             # Home page layout and section spacing
│   │   ├── SignIn/
│   │   │   ├── SignIn.jsx           # Login form — email/password inputs, Firebase signIn, error toasts
│   │   │   └── SignIn.css           # Netflix dark card login styling
│   │   └── SignUp/
│   │       ├── SignUp.jsx           # Registration form — Firebase createUser call, redirect on success
│   │       └── SignUp.css           # Sign up page styling consistent with SignIn
│   ├── firebase.js                  # Firebase app init — exports `auth` instance for use across components
│   ├── App.jsx                      # Root — Router setup, useAuthState guard, all route definitions
│   └── main.jsx                     # React DOM entry point
├── index.html                       # Vite HTML entry point
├── vite.config.js                   # Vite + React plugin configuration
├── eslint.config.js                 # ESLint rules — React, hooks, and refresh plugins
└── package.json                     # Dependencies and npm scripts
```

---

## 🚀 Getting Started

**Prerequisites:** Node.js 18+ and a Firebase project with the **Email/Password** sign-in provider enabled.

**1. Clone the repository**
```bash
git clone https://github.com/tripathipawan/Netflix_Clone.git
cd Netflix_Clone
```

**2. Install dependencies**
```bash
npm install
```

**3. Configure Firebase**

Create a `.env` file in the root directory with your Firebase project credentials:

```env
VITE_FIREBASE_API_KEY=your_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
```

Get these from [Firebase Console](https://console.firebase.google.com) → Your Project → Project Settings → Your Apps → Web App config. Then enable **Email/Password** under Authentication → Sign-in method.

**4. Start the development server**
```bash
npm run dev
```

**5. Build for production**
```bash
npm run build
```

---

## 🎮 How to Use

1. Open the app — the sign-in page loads by default for unauthenticated users.
2. Click **Sign Up** to register a new account with email and password.
3. On successful registration, you are automatically signed in and redirected to the **Home** page.
4. Browse the Netflix-style layout — hero banner, multiple category rows, hover effects on movie cards.
5. Click **Sign Out** in the navbar — a success toast appears and you are redirected to sign-in.
6. Sign back in — your session is restored instantly from Firebase's persisted token.

---

## 🧠 Architecture Highlights

| Concern | Implementation |
|---|---|
| Auth State Binding | `useAuthState(auth)` from `react-firebase-hooks` — returns `[user, loading, error]` reactively |
| Protected Routes | `App.jsx` reads `user` from `useAuthState`; uses `<Navigate>` for auth-state-based redirects |
| Sign Up | `createUserWithEmailAndPassword(auth, email, password)` — errors caught per Firebase error codes |
| Sign In | `signInWithEmailAndPassword(auth, email, password)` — Firebase error codes mapped to toast messages |
| Session Persistence | Firebase Auth persists the JWT in `localStorage` by default — auto-restored on page refresh |
| Sign Out | `signOut(auth)` clears Firebase session → `useAuthState` updates → Router redirects to `/signin` |
| Toast System | `<ToastContainer>` in `App.jsx`; `toast.success()` / `toast.error()` called from all auth handlers |

---

## 🌱 What I Learned

- Building a complete Firebase email/password authentication flow — registration, login, session persistence, and logout — connected to a live backend
- Using `react-firebase-hooks` to bind Firebase Auth's real-time state observer directly into React's component lifecycle via `useAuthState`
- Implementing auth-state-based protected routing in React Router — redirecting users based on whether they are authenticated or not
- Mapping Firebase error codes to user-friendly toast messages for a polished authentication UX
- Replicating a complex, production-level UI (Netflix's design system) using only vanilla CSS — hero layout, horizontal scroll rows, card hover animations

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature-name`)
3. Commit your changes (`git commit -m 'Add: your feature description'`)
4. Push to the branch (`git push origin feature/your-feature-name`)
5. Open a Pull Request

---

## 👨‍💻 Author

**Pawan Tripathi**
- GitHub: [@tripathipawan](https://github.com/tripathipawan)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
