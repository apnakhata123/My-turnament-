# Gaming Tournament Admin Panel Android App

A high-performance Android administrative application delivering the complete Gaming Tournament Admin Panel experience with pixel-perfect neomorphic design, full Firebase Realtime Database and Auth integration, and complete feature parity for tournament, user, and financial operations.

### User Review & Critical Decisions

> [!IMPORTANT]
> The admin configuration and architectural choices have been aligned with your preferences:
> - **Admin Account Creation & Authentication**: First-time launch checks `/adminConfig`. If unconfigured, the **Admin Account Setup** screen is presented to establish your desired admin email and password. Once initialized, the secure **Admin Login** gate protects all operations.
> - **Visual Style Preservation**: Retains the exact neomorphic soft-shadow aesthetic (`--nm-bg: #e8ebf2`), custom neomorphic animated loaders, responsive offcanvas drawer, and Material 3 Android wrapper.
> - **Full Management Suite**: Complete implementation across all 20 modules (Tournaments, Prize Distribution, Users, Withdrawals, Verifications, Staff, Analytics, Promo Codes, Bank Details, and Realtime Settings).

---

## 1. Overview & Core Concept

- **What It Does**: Provides tournament administrators with a mobile management console to create games, schedule tournaments, publish room IDs/passwords, manage player entries, credit per-kill and rank prizes, approve/reject withdrawals with automated refund handling, review Free Fire verifications, and broadcast global push alerts.
- **Target Audience**: Gaming tournament organizers, esports community owners, and app administrators.
- **Backend & Cloud Services**: Connected to Firebase project `turnament-app-my` via Firebase Realtime Database and Firebase Authentication.

---

## 2. User Experience & Visual Design

- **Visual Identity**:
  - *Aesthetic*: Soft neomorphic light theme with dual extruded shadows (`7px 7px 16px #c2c6d2, -7px -7px 16px #ffffff`), inset text inputs, and vibrant golden yellow (`#FACC15`) and royal blue (`#3B82F6`) accents.
  - *Typography*: Poppins font family across headers, metric cards, and data tables.
  - *Responsive Layout*: Fixed top navigation bar with offcanvas sidebar menu, quick stats cards, interactive Chart.js visualizations, and responsive data tables with copy-to-clipboard conveniences.
- **Key Modules**:
  1. **Dashboard Overview**: Live counter cards (Total Users, Active/Upcoming Tournaments, Withdrawals, Games, Staff) and 7-day user signup trend chart.
  2. **Auth & Theme Customization**: 10 live theme presets (Neo Light, Neo Dark, Ocean Blue, Gaming Red, Emerald, etc.), custom RGB color pickers, and user-app login switches.
  3. **Tournament & Prize Management**: Game creation, match scheduling (Solo/Duo/Squad, slots, entry fees, prize pools, room credentials), registered player review, per-kill/rank winnings distribution, and match history logging.
  4. **Financial Operations**: Pending/Completed/Rejected withdrawal approvals with reason inputs, bank account manager (PhonePe, GPay, Paytm, Bank/IFSC), and transaction invoice modals.
  5. **User & Staff Directory**: User lookup, balance adjustments (Total, Winning, Bonus) with transaction audit trail, account blocking, secondary staff account creation, and PDF report downloads.
  6. **Engagement & Social**: Global/individual notification dispatcher with ImgBB image uploads, social links editor (Telegram, YouTube, WhatsApp), and promo code engine.

---

## 3. Technical Architecture & Data Strategy

```
┌────────────────────────────────────────────────────────┐
│             Android Native Container                   │
│   MainActivity (Edge-to-Edge, File Chooser Picker)     │
└──────────────────────────┬─────────────────────────────┘
                           │
┌──────────────────────────▼─────────────────────────────┐
│       High-Performance Local Web Container             │
│   • Assets: admin_panel.html (Neomorphic UI + JS)      │
│   • Bootstrap 5, Chart.js, jsPDF, Bootstrap Icons      │
└──────────────────────────┬─────────────────────────────┘
                           │
┌──────────────────────────▼─────────────────────────────┐
│          Firebase Realtime Services                    │
│   • Auth: Email/Password login & setup verification    │
│   • RTDB (turnament-app-my-default-rtdb):              │
│       /adminConfig          /tournaments               │
│       /users                /withdrawals               │
│       /games                /transactions              │
│       /notifications        /settings                  │
│       /staff                /promoCodes                │
└────────────────────────────────────────────────────────┘
```

- **File Upload Handler**: `WebChromeClient.onShowFileChooser` connected to Android's `ActivityResultContracts.GetContent` / `StartActivityForResult` allowing seamless camera and photo gallery uploads directly into the ImgBB uploader.
- **Android Manifest & Permissions**: Adds `<uses-permission android:name="android.permission.INTERNET" />` and `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`.
- **Hardware Acceleration**: Enabled on WebView with local storage, DOM storage, and caching.

---

## 4. Execution Steps

1. **Permissions & Configuration**: Update `AndroidManifest.xml` with Internet permissions and hardware acceleration. Set app label to "Tournament Admin" in `strings.xml` and sync `metadata.json`.
2. **Asset Deployment**: Place the complete, styled `admin_panel.html` inside `app/src/main/assets/admin_panel.html` with Firebase credentials, neomorphic styling, and full scripts.
3. **Android Native Host (`MainActivity.kt`)**: Implement WebView container with JavaScript enabled, DOM storage, WebChromeClient for photo/file picking, download listener, and back-press handling.
4. **Build Verification**: Run `compile_applet` to ensure APK builds cleanly and launches reliably.
