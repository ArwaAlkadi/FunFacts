# FunFacts

**One fact a day, right on your lock screen.**

FunFacts is an iOS app that delivers a unique daily fun fact through local notifications, based on the user's selected interest. It combines learning and entertainment in a colorful, playful interface built with SwiftUI.


<br>
<img width="1920" height="1080" alt="Funfacts2025" src="https://github.com/user-attachments/assets/e4c62727-62d5-431a-94ed-f2d4c86fcae5" />
<br>

## Features

- **Daily fact notifications** — a new fact arrives every day at the user's chosen time
- **Interest categories** — Nature, Human, Random, and Lifestyle
- **Personal profile** — pick a name and an animal avatar from a collection of 17
- **Coin economy** — start with 10 coins, earn more by sharing facts, and spend them to unlock new avatars
- **Onboarding flow** and a fully offline experience — no account, no server

## How It Works

Since iOS limits pending local notifications to 64 per app, FunFacts **batch-schedules up to 64 days of facts ahead** in one pass — each notification carrying its own fact, personalized with the user's name and category. The fact of the day is picked deterministically from the category's list using the day of the year, so every day is guaranteed a different fact and the schedule never repeats itself back-to-back.

All state — name, avatar, interests, coins, and owned avatars — lives in a single `AppState` observable object persisted with UserDefaults, keeping the app simple and completely offline.

## Architecture

```
FunFacts
├── Core/            # AppState (UserDefaults persistence),
│                    # FactsArrays (categorized facts),
│                    # Notifications (64-day batch scheduler)
└── Views/           # Splash, Onboarding, Sign in, Interests,
                     # Fun fact page, Profile, Edit profile
```

## Tech Stack

- Swift · SwiftUI
- UserNotifications (`UNUserNotificationCenter`) for daily local notifications
- UserDefaults for local persistence
- `@EnvironmentObject` / `@Published` state management, `NavigationStack` navigation
