# Google Play Data Safety Declaration

**App:** Family Shopping List
**Date:** 2026-02-14

---

## Account Creation Methods

- **Username and password** — Email + password registration via Firebase Auth
- **OAuth** — Google Sign-In

---

## Account Deletion

**URL:** https://sinful1992.github.io/familyshoppinglist-legal/delete-account.html

Users can delete their account in-app via Settings > Delete Account. All personal data is permanently removed immediately.

---

## Data Types Declared

### Personal Info

| Data Type | Declared |
|---|---|
| Name | Yes |
| Email address | Yes |
| User IDs | Yes |
| Address | No |
| Phone number | No |
| Race and ethnicity | No |
| Political or religious beliefs | No |
| Sexual orientation | No |
| Other info | No |

### Financial Info

| Data Type | Declared |
|---|---|
| User payment info | No |
| Purchase history | Yes |
| Credit score | No |
| Other financial info | No |

### Photos and Videos

| Data Type | Declared |
|---|---|
| Photos | Yes |

> **Declared (corrected 2026-10):** receipt photos leave the device. They are uploaded to Firebase Cloud Storage
> (`receipts/{familyGroupId}/{listId}/{ts}.jpg`, ImageStorageManager) and, when scanned, sent via the Supabase
> `ocr-proxy` edge function to the receipt OCR service on Hugging Face (ReceiptOCRService). Play answers:
> **collected: yes, shared: no** (Google, Supabase and Hugging Face act as service providers), purpose
> **App functionality**, **optional** (scanning a receipt is the user's choice).

### Calendar

| Data Type | Declared |
|---|---|
| Calendar events | No |

### App Activity

| Data Type | Declared |
|---|---|
| App interactions | Yes |
| In-app search history | No |
| Installed apps | No |
| Other user-generated content | Yes |
| Other actions | No |

### App Info and Performance

| Data Type | Declared |
|---|---|
| Crash logs | Yes |
| Diagnostics | Yes |
| Other app performance data | No |

### Device or Other IDs

| Data Type | Declared |
|---|---|
| Device or other IDs | Yes |

---

## Detailed Disclosure Per Data Type

### Name (Display Name)

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Optional — users can leave display name blank |
| Why collected | App functionality, Account management |
| Why shared | App functionality |

**Explanation:** Display names are stored in Firebase Realtime Database so family group members can identify each other in shared shopping lists. It's optional — users can use the app without setting a name.

---

### Email Address

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Required |
| Why collected | App functionality, Account management |
| Why shared | App functionality, Account management |

**Explanation:** Email is required for Firebase Authentication — users must provide an email to create an account and sign in. Shared with Firebase (Google) for authentication and credential verification.

---

### User IDs

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Required |
| Why collected | App functionality, Account management |
| Why shared | App functionality, Account management |

**Explanation:** Firebase UID is auto-generated on account creation. Stored in Firebase RTDB to link users to their data (lists, items, family groups). Shared with RevenueCat to manage subscriptions tied to the correct user.

---

### Purchase History

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Optional — users can add items without prices |
| Why collected | App functionality |
| Why shared | App functionality |

**Explanation:** Shopping list item names and prices that users manually enter are synced to Firebase RTDB for real-time collaboration. Shared with family group members so they can see shared shopping lists. Prices are optional. Receipt images are covered under Photos (uploaded to Firebase Cloud Storage; scans are read by the OCR service via Supabase).

---

### App Interactions

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Required |
| Why collected | Analytics |
| Why shared | Analytics |

**Explanation:** Firebase Analytics tracks screen views and feature usage events (e.g., list created, item checked, receipt captured, paywall viewed). Used to understand how the app is used and improve features. Users cannot opt out.

---

### Other User-Generated Content

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Required |
| Why collected | App functionality |
| Why shared | App functionality |

**Explanation:** Shopping lists, items, family group data, and urgent items are the core content of the app. Stored in Firebase RTDB and synced across family group members for real-time collaborative shopping. This is the primary purpose of the app.

---

### Crash Logs

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Required |
| Why collected | Analytics |
| Why shared | Analytics |

**Explanation:** Firebase Crashlytics collects crash reports including stack traces and error logs. Used to monitor app stability and fix crashes. Users cannot opt out.

---

### Diagnostics

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Required |
| Why collected | Analytics |
| Why shared | Analytics |

**Explanation:** Firebase Crashlytics collects device model, OS version, app version, and custom attributes for debugging. Used to diagnose bugs and understand crash context. Users cannot opt out.

---

### Device or Other IDs

| Field | Answer |
|---|---|
| Collected | Yes |
| Shared | Yes |
| Processed ephemerally | No |
| Required or optional | Required (free tier: advertising ID via AdMob); push tokens are optional |
| Why collected | App functionality, Advertising or marketing |
| Why shared | App functionality, Advertising or marketing |

**Explanation:** FCM device tokens are collected when users enable push notifications for urgent shopping items. Tokens are stored in Supabase and used to deliver notifications via Firebase Cloud Messaging. Users can choose not to enable notifications.

**Advertising ID (AdMob):** on the free tier the Google Mobile Ads SDK (rewarded ads before a receipt scan or urgent item) collects the Android advertising ID and shares it with Google for ad serving, measurement, fraud prevention and, with UMP consent in the UK/EEA, personalisation. The merged manifest declares `com.google.android.gms.permission.AD_ID` and `ACCESS_ADSERVICES_AD_ID`. Premium/Family users: the SDK is not initialised.

---

## Third-Party Services

| Service | Provider | Data Received | Purpose |
|---|---|---|---|
| Firebase Authentication | Google | Email, password hash | User sign-in |
| Firebase Realtime Database | Google | User IDs, names, lists, items, prices | Data sync |
| Firebase Analytics | Google | Screen views, usage events, user ID | Analytics |
| Firebase Crashlytics | Google | Crash logs, diagnostics, device info | Crash reporting |
| Firebase Cloud Messaging | Google | FCM device tokens | Push notifications |
| Supabase | Supabase Inc. | FCM tokens, user ID, family group ID | Push notification delivery |
| RevenueCat | RevenueCat Inc. | User ID, subscription status | Subscription management |
| Google Play Billing | Google | Payment info (not accessed by app) | In-app purchases |
| Receipt OCR (Supabase ocr-proxy → Hugging Face Space) | Supabase Inc., Hugging Face | Receipt photo | Reading receipts (service provider) |
| Google AdMob | Google | Advertising ID, IP address, device info, ad interactions | Rewarded ads on the free tier (personalised only with consent) |

---

## Data NOT Collected

- Location data
- Payment card details (handled by Google Play)
- Contacts, calendar, phone data
- Videos
- Search history
- Installed apps
- Audio, files, or documents
