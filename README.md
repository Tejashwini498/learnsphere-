# LearnSphere 🎓

An online e-learning platform that connects **learners** with structured skill-building programs, and gives **admins** the tools to create and manage those programs — built with Flutter.

## Project Overview & Purpose

Learners often struggle to find trustworthy, well-structured programs in one place, and tend to drop off midway due to a lack of clear progress tracking. Program creators, in turn, lack a lightweight way to publish and monitor content without heavy tooling.

LearnSphere solves both sides of that problem in a single mobile app:

- **Learners** discover, enroll in, and track progress through curated programs, and earn certificates on completion.
- **Admins** create, publish, and manage programs, and monitor enrollment and learner activity from a dashboard.

## Features

**Learner-facing**
- Email/password login and sign-up (with inline validation)
- Home feed — continue-learning card, category browsing, recommended programs
- Program Listing — live search + category filter chips
- Program Details — curriculum accordion, ratings, Enroll action
- Progress tracker for enrolled programs
- Feedback form — star rating + comments, submitted per enrolled program
- Profile & logout

**Admin-facing** *(shown automatically for any login email starting with `admin`, e.g. `admin@learnsphere.com`)*
- Dashboard with total programs, active enrollments, and average rating
- Program management list (edit/delete menu scaffold)

## Tech Stack

- **Framework:** Flutter (Dart), Material 3
- **State management:** Provider (`AuthService`, `ProgramService` as `ChangeNotifier`s)
- **Data layer:** In-memory mock service layer that mimics real API latency (`Future.delayed`) — built so the same method signatures (`fetchPrograms`, `enroll`, `submitFeedback`, `login`) can be swapped for real `http`/Firebase calls without touching the UI.

## Project Structure

```
learnsphere/
├── lib/
│   ├── main.dart                          # App entry point, Provider setup
│   ├── models/
│   │   ├── user_model.dart                # AppUser, UserRole
│   │   └── program_model.dart             # Program, CurriculumModule
│   ├── screens/
│   │   ├── splash_screen.dart
│   │   ├── login_screen.dart
│   │   ├── signup_screen.dart
│   │   ├── home_screen.dart               # Bottom-nav shell + Home tab
│   │   ├── program_listing_screen.dart
│   │   ├── program_details_screen.dart
│   │   ├── progress_screen.dart
│   │   ├── profile_screen.dart
│   │   ├── feedback_screen.dart           # Required Week 4 form
│   │   └── admin_dashboard_screen.dart
│   ├── widgets/
│   │   ├── custom_button.dart
│   │   ├── custom_text_field.dart
│   │   └── program_card.dart
│   ├── services/
│   │   ├── auth_service.dart              # Mock auth (Provider ChangeNotifier)
│   │   └── program_service.dart           # Mock programs/enroll/feedback data
│   └── utils/
│       ├── constants.dart
│       └── theme.dart                     # Centralized branding/colors
├── assets/
├── test/
│   └── widget_test.dart
├── pubspec.yaml
└── README.md
```

## Navigation Flow

```
Splash Screen
   └── Login / Sign Up
         └── Home (Learner)  — bottom nav: Home | Programs | Progress | Profile
               ├── Program Listing → Program Details → Enroll → Feedback Form
               ├── Progress (enrolled programs)
               └── Profile → Logout

         └── Admin Dashboard (admin@... login)
               ├── Enrollment & rating overview
               └── Manage Programs (edit/delete menu)
```

## Setup Instructions

1. **Prerequisites:** [Flutter SDK](https://docs.flutter.dev/get-started/install) 3.19+ and Dart 3+.
2. **Clone and install dependencies:**
   ```bash
   git clone https://github.com/<your-username>/learnsphere.git
   cd learnsphere
   flutter pub get
   ```
3. **Run the app** on a connected device/emulator:
   ```bash
   flutter run
   ```
4. **Run tests:**
   ```bash
   flutter test
   ```
5. **Try both roles:**
   - Learner login: any email/password (e.g. `sonia@example.com` / `test123`)
   - Admin login: any email starting with `admin` (e.g. `admin@learnsphere.com` / `test123`)

## Screenshots

> Add screenshots here before final submission, e.g.:
>
> | Login | Home | Program Details | Feedback |
> |---|---|---|---|
> | `screenshots/login.png` | `screenshots/home.png` | `screenshots/details.png` | `screenshots/feedback.png` |

## Changelog

- **v1.0.0 (Week 4 — Final):** Full navigation across all screens, feedback form with validation, Progress and Profile tabs, Admin Dashboard, consistent branding/theme applied app-wide, mock data-service layer ready for backend swap.
- **v0.3.0 (Week 3):** Navigation wiring between screens, Provider-based state management introduced.
- **v0.2.0 (Week 2):** Static UI built for Login, Home, Program Listing, and Program Details screens.
- **v0.1.0 (Week 1):** App proposal, wireframes, Flutter project scaffolding, and GitHub repo setup.

## Roadmap Status

- [x] Week 1: App proposal, wireframes, project & repo setup
- [x] Week 2: Static UI for core screens
- [x] Week 3: Navigation + state management wiring
- [x] Week 4: Full app, feedback form, polished README, final submission

## Reflection

Building LearnSphere over four weeks was a hands-on introduction to shipping a real Flutter app end to end — starting from a proposal and low-fidelity wireframes, through static UI, then wiring up navigation and state management with Provider, and finally connecting a (mock) data layer with forms and validation. The biggest challenges were structuring the codebase so screens, widgets, and services stayed cleanly separated, and designing a service layer that behaves like a real API (with latency and error states) so it can be swapped for a real backend later without rewriting the UI. This project is now a portfolio-ready piece I can point to when talking about my Flutter/mobile development experience.
