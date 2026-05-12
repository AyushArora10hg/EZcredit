# EZCredit

## Debt Recovery System

**A comprehensive Android solution for small and mid-sized businesses to manage customers, invoices, payments, and credit operations.**

[![Kotlin](https://img.shields.io/badge/Kotlin-2.0-blue?logo=kotlin&logoColor=white)](https://kotlinlang.org/)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-UI-blueviolet?logo=android&logoColor=white)](https://developer.android.com/jetpack/compose)
[![Firebase](https://img.shields.io/badge/Firebase-Backend-orange?logo=firebase&logoColor=white)](https://firebase.google.com/)
[![WorkManager](https://img.shields.io/badge/WorkManager-Background-green?logo=android&logoColor=white)](https://developer.android.com/topic/libraries/architecture/workmanager)
[![Stripe](https://img.shields.io/badge/Stripe-Payments-0A2540?logo=stripe&logoColor=white)](https://stripe.com/)
[![OCR](https://img.shields.io/badge/OCR-Gemini-FFBB33?logo=google&logoColor=white)](https://developers.google.com/)

---

## Quick Links

- [Download APK](https://drive.google.com/file/d/18__9RzaufhRY0M1HGlIvEj9O_pxsm4-J/view?usp=sharing)
- [View Source Code](https://github.com/DakshArora07/Android_EZcredit)
- [Final Presentation](https://youtu.be/iZ0tL8lbQ88)
- [Project Pitch](https://youtu.be/o5EsZg6VefA)
- [Show and Tell 1](https://youtu.be/CRAPZDmeTiM)
- [Show and Tell 2](https://youtu.be/5QegMo8JUec)

---

## Overview

EZCredit is a modern Android application built to streamline financial operations for small and mid-sized businesses. The platform provides an end-to-end solution for managing customer relationships, processing invoices, accepting payments, and maintaining credit records across multiple companies and users.

### Core Capabilities

The application delivers a complete business workflow including company creation, multi-user access control, customer management, invoice processing, automated payment reminders, integrated payment processing via Stripe, automatic receipt generation, intelligent background task automation, and real-time data synchronization across devices.

Built on Firebase for cloud infrastructure and Room for local persistence, EZCredit ensures data consistency across multiple users and devices. While basic functionality is available offline, advanced features including invoice synchronization, user management, payment processing, and background automation require an active internet connection.

---

## Key Features

### Multi-Company & Multi-User Architecture

- Create and manage multiple companies from a single application
- Role-based access control with three permission levels: Admin, Sales, and Receipts
- Isolated data environments per company with real-time synchronization
- Seamless company switching with instant dataset updates

### User & Company Management

- Comprehensive admin controls for company settings, user management, and access permissions
- Self-service profile management for all users
- Context-aware UI that adapts to user permissions:
  - **Sales Role:** Access to customer and invoice management
  - **Receipts Role:** Limited to receipt processing
  - **Admin Role:** Full system access and configuration

### Intelligent Invoice Management

- Manual invoice creation with comprehensive data entry
- OCR-powered invoice extraction from images and camera input
- Automated status tracking (Unpaid, Paid, Past Due, Late)
- Advanced filtering and sorting capabilities
- Full invoice lifecycle management including editing and deletion
- Professional PDF invoice generation
- Automated email reminders with integrated payment links

### Optical Character Recognition (OCR)

- Precise text extraction from invoice images
- Automated field population for invoice amounts, dates, and customer information
- Support for both camera capture and image uploads
- Pure text extraction without AI interpretation to ensure accuracy

### Payment Processing & Receipt Automation

- Integrated Stripe payment gateway for secure online transactions
- Email-based payment links for customer convenience
- Automatic cloud-based receipt generation upon successful payment
- Real-time receipt synchronization across all company users
- Manual receipt creation for cash and in-person transactions
- Comprehensive receipt search and filtering

### Analytics Dashboard

- Executive-level insights for admin users including:
  - Total revenue collected
  - Past-due payment trends
  - Outstanding balance tracking
  - Customer credit performance metrics
- Flexible time-based filtering (weekly, monthly, quarterly views)

### Calendar View

- Visual invoice tracking on calendar interface
- Multi-status filtering (Paid, Unpaid, Past Due, Late)
- Quick navigation through payment history
- At-a-glance financial overview

### Background Automation System

Five intelligent workers handle critical business operations automatically:

| Worker | Function |
|--------|----------|
| **Auto Email Reminder** | Sends daily payment reminders via Mailgun API |
| **Credit Score Update** | Recalculates customer credit scores based on payment history |
| **Overdue Invoice** | Automatically marks invoices as past due when deadlines pass |
| **Paid/Late Payment** | Matches receipts with invoices and updates payment status |
| **Daily Summary** | Generates notification summaries of updates across app |

---

## Technology Stack

### Frontend Technologies

- **Language:** Kotlin 2.0
- **UI Framework:** Jetpack Compose with Material 3 Design
- **Architecture:** MVVM with Clean Architecture principles
- **State Management:** StateFlow and Kotlin Coroutines
- **Background Processing:** WorkManager
- **PDF Generation:** iText library with FileProvider
- **OCR Engine:** Google Gemini 1.5 Flash

### Backend & Cloud Services

- **Authentication:** Firebase Authentication
- **Cloud Database:** Cloud Firestore
- **Local Storage:** Room Database
- **File Storage:** Firebase Cloud Storage
- **Email Service:** Mailgun API
- **Payment Gateway:** Stripe API
- **AI Processing:** Google Gemini Messages API

---

## Architecture

### Application Architecture

```
┌─────────────────────────────────────┐
│ UI Layer (Jetpack Compose)          │
│ • Material 3 Design System           │
│ • Declarative UI Components          │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ ViewModel Layer                     │
│ • Business Logic                     │
│ • Lifecycle-Aware Components         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ Repository Layer                     │
│ • Data Source Abstraction            │
│ • IO Dispatcher Operations           │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ External Services                    │
│ Firebase • Stripe • Mailgun • Room   │
└─────────────────────────────────────┘
```

### MVVM Architecture

![MVVM Architecture Diagram 1](./docs/MVVM1.png)
![MVVM Architecture Diagram 2](./docs/MVVM2.png)

### Threading Model

![Threading Architecture](./docs/Threads.png)

### Cloud Database Structure

```
Firebase Realtime Database Structure (EZCredit)

ROOT
└── companies/
    └── {companyId}/
        ├── users/
        │   └── {userId}/
        │       ├── name: "John Doe"
        │       ├── email: "john@company.com"
        │       ├── companyId: 1
        │       ├── accessLevel: "Admin"
        │       ├── lastModified: 1733100000000
        │       └── isDeleted: false
        │
        └── data/
            ├── customers/
            │   └── {customerId}/
            │       ├── name: "Acme Corp"
            │       ├── email: "billing@acme.com"
            │       ├── companyId: 1
            │       ├── lastModified: 1733100000000
            │       └── isDeleted: false
            │
            ├── invoices/
            │   └── {invoiceId}/
            │       ├── invoiceNumber: "INV-001"
            │       ├── customerId: 123
            │       ├── amount: 2500.00
            │       ├── companyId: 1
            │       ├── lastModified: 1733100000000
            │       └── isDeleted: false
            │
            └── receipts/
                └── {receiptId}/
                    ├── receiptNumber: "AUTO_REC_001"
                    ├── invoiceId: "INV-001"
                    ├── receiptDate: 1733100000000
                    ├── companyId: 1
                    ├── lastModified: 1733100000000
                    └── isDeleted: false
```

### Project Structure

```
EZCredit/
├── data/
│   ├── dao/                # Data Access Objects (5 classes)
│   ├── entity/             # Data Models
│   ├── repository/         # Repository Implementations (5 classes)
│   └── viewmodel/          # database view models and factories (10 classes)
│
├── ui/
│   ├── screens/            # Jetpack Compose Screens
│   ├── viewmodel/          # ViewModels (12 classes)
│   └── theme/              # Material 3 Theme (3 classes)
│
├── workers/                # WorkManager Background Workers (5 classes)
│
└── utils/                  # Utility Classes (OCR, Date Helpers, etc.)
```

---

## Development Team

| Team Member | Responsibilities |
|-------------|-----------------|
| **Ayush Arora** | UI Design, WorkManager Implementation, Credit Score Algorithm, Email Reminder System |
| **Daksh Arora** | Room Database Architecture, Firebase Synchronization, Firebase Authentication, Cloud Functions, Payment Gateway Integration |
| **Gurshan Singh Aulakh** | Invoice & Customer UI Development, Automated Email Worker, PDF Invoice Generation |
| **Hetmay Vora** | Calendar Interface, Analytics Dashboard, Authentication UI, Company and User Profile Screens |
| **Henry Nguyen** | OCR Engine Development, Invoice Formatting, Receipt Interface, Architecture Documentation |

---

## 📄 License

This project is developed as part of an academic course assignment for educational purposes.


---

**Built with ❤️ for Android Development Course**

*Last Updated: December 2025*
