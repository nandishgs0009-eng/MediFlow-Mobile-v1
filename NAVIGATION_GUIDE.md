# MedMinder Navigation & Routes Guide

## 📍 Complete Navigation Structure

### Main Routes
```
/ .......................... Landing Page
/login ..................... Login Page
/signup .................... Sign Up Page
/dashboard ................. Main Dashboard (Protected)
/treatments ................ My Treatments (Protected)
/history ................... Medication History (Protected)
/recovery-reports .......... Recovery Reports & Analytics (Protected)
```

### Settings Routes (Accessible via Settings Dropdown)
```
/profile ................... Patient Profile (Protected)
/notifications ............. Notification Preferences (Protected)
/medical-records ........... Medical Records (Protected)
/health-summary ............ Health Summary Report (Protected)
```

---

## 🔗 Settings Dropdown Links

All main pages have a **Settings dropdown** in the sidebar with links to:

### Updated Pages with Full Navigation:
✅ **Dashboard** (`src/pages/Dashboard.tsx`)
- Profile → `/profile`
- Notifications → `/notifications`
- Medical Records → `/medical-records`
- Health Summary → `/health-summary`

✅ **History** (`src/pages/History.tsx`)
- Profile → `/profile`
- Notifications → `/notifications`
- Medical Records → `/medical-records`
- Health Summary → `/health-summary`

✅ **Recovery Reports** (`src/pages/RecoveryReports.tsx`)
- Profile → `/profile`
- Notifications → `/notifications`
- Medical Records → `/medical-records`
- Health Summary → `/health-summary`

✅ **My Treatments** (`src/pages/MyTreatments.tsx`)
- Profile → `/profile`
- Notifications → `/notifications`
- Medical Records → `/medical-records`
- Health Summary → `/health-summary`

✅ **Profile** (`src/pages/Profile.tsx`)
- Profile → `/profile` (Current page - highlighted)
- Notifications → `/notifications`
- Medical Records → `/medical-records`
- Health Summary → `/health-summary`

✅ **Notifications** (`src/pages/Notifications.tsx`)
- Profile → `/profile`
- Notifications → `/notifications` (Current page - highlighted)
- Medical Records → `/medical-records`
- Health Summary → `/health-summary`

---

## 📋 Pages & Their Features

### 1️⃣ **Dashboard** (`/dashboard`)
- Overview of medication statistics
- Weekly adherence chart
- Daily medication status
- Quick access to treatments and history
- Settings dropdown menu

### 2️⃣ **My Treatments** (`/treatments`)
- View all active treatments
- Manage medicines
- Confirm medication intake
- Track stock levels
- Settings dropdown menu

### 3️⃣ **History** (`/history`)
- View medication intake history
- Filter by date
- Search by medicine name
- Filter by treatment (URL parameter)
- Settings dropdown menu

### 4️⃣ **Recovery Reports** (`/recovery-reports`)
- Overall adherence metrics
- Recovery percentage calculation
- Multiple chart types
- Treatment statistics
- Settings dropdown menu

### 5️⃣ **Profile** (`/profile`) ⭐ NEW
- **View Mode**: Display all patient information
- **Edit Mode**: Update patient details
- Editable fields:
  - Full Name
  - Phone Number
  - Date of Birth
  - Gender
  - Blood Type
  - Height & Weight (BMI Calculation)
  - Medical Conditions
  - Allergies
  - Medications Notes
  - Address Information
  - Emergency Contact Details
- Read-only Email
- Auto-calculated Age & BMI with status indicators
- Settings dropdown menu

### 6️⃣ **Notifications** (`/notifications`) ⭐ NEW
- Notification preferences (7 toggles):
  - Medicine Reminders
  - Appointment Alerts
  - Low Stock Warnings
  - Weekly Reports
  - Health Alerts
  - Email Notifications
  - Push Notifications
- Recent notifications list
- Mark as read functionality
- Delete individual notifications
- Clear all notifications
- Settings dropdown menu

### 7️⃣ **Medical Records** (`/medical-records`) ⭐ NEW
- Document upload section (placeholder)
- Medical records list
- Filter by type
- Search functionality
- Download/view records
- Delete records
- Add new records
- Settings dropdown menu

### 8️⃣ **Health Summary** (`/health-summary`) ⭐ NEW
- Overall health status card
- Key health metrics
- Recent measurements
- Health trends chart
- Recommendations section
- Medical alerts
- Export to PDF option
- Settings dropdown menu

---

## 🎯 Quick Access Map

```
┌─ Dashboard
│  ├─ Settings ▼
│  │  ├─ Profile
│  │  ├─ Notifications
│  │  ├─ Medical Records
│  │  └─ Health Summary
│  ├─ My Treatments
│  ├─ History
│  └─ Recovery Reports
│
├─ My Treatments
│  ├─ Settings ▼
│  │  ├─ Profile
│  │  ├─ Notifications
│  │  ├─ Medical Records
│  │  └─ Health Summary
│  ├─ Dashboard
│  ├─ History
│  └─ Recovery Reports
│
├─ History
│  ├─ Settings ▼
│  │  ├─ Profile
│  │  ├─ Notifications
│  │  ├─ Medical Records
│  │  └─ Health Summary
│  ├─ Dashboard
│  ├─ My Treatments
│  └─ Recovery Reports
│
└─ Recovery Reports
   ├─ Settings ▼
   │  ├─ Profile
   │  ├─ Notifications
   │  ├─ Medical Records
   │  └─ Health Summary
   ├─ Dashboard
   ├─ My Treatments
   └─ History
```

---

## 🔐 Protected Routes

All routes except `/`, `/login`, `/signup`, and `/landing` require authentication.

Routes protected by `<ProtectedRoute>` component:
- `/dashboard`
- `/treatments`
- `/history`
- `/recovery-reports`
- `/profile`
- `/notifications`
- `/medical-records`
- `/health-summary`

---

## 🚀 How to Navigate

1. **From Main Navigation Sidebar**: Click on MAIN/MENU items
2. **From Settings Dropdown**: Click Settings icon, then select submenu item
3. **Direct URL**: Type route in browser address bar (e.g., `localhost:5173/profile`)

---

## 📱 Responsive Design

All pages are fully responsive:
- Desktop: Full sidebar visible with all text
- Tablet: Sidebar with icon labels
- Mobile: Sidebar can be collapsed to icons only

---

## 🔗 Route Configuration

Defined in `src/App.tsx`:

```tsx
<Routes>
  {/* Public Routes */}
  <Route path="/" element={<Index />} />
  <Route path="/login" element={<Auth />} />
  <Route path="/signup" element={<Auth />} />
  
  {/* Protected Routes */}
  <Route path="/dashboard" element={<ProtectedRoute><Dashboard /></ProtectedRoute>} />
  <Route path="/treatments" element={<ProtectedRoute><MyTreatments /></ProtectedRoute>} />
  <Route path="/history" element={<ProtectedRoute><History /></ProtectedRoute>} />
  <Route path="/recovery-reports" element={<ProtectedRoute><RecoveryReports /></ProtectedRoute>} />
  <Route path="/profile" element={<ProtectedRoute><Profile /></ProtectedRoute>} />
  <Route path="/notifications" element={<ProtectedRoute><Notifications /></ProtectedRoute>} />
  <Route path="/medical-records" element={<ProtectedRoute><MedicalRecords /></ProtectedRoute>} />
  <Route path="/health-summary" element={<ProtectedRoute><HealthSummary /></ProtectedRoute>} />
  
  {/* 404 */}
  <Route path="*" element={<NotFound />} />
</Routes>
```

---

## ✅ Navigation Status

| Feature | Status | Notes |
|---------|--------|-------|
| Main Navigation Links | ✅ Complete | Dashboard, Treatments, History, Reports |
| Settings Dropdown | ✅ Complete | All 4 settings items linked |
| Profile Navigation | ✅ Complete | All links working |
| Notifications Navigation | ✅ Complete | All links working |
| Medical Records Navigation | ✅ Complete | All links working |
| Health Summary Navigation | ✅ Complete | All links working |
| Protected Routes | ✅ Complete | Authentication required |
| Responsive Design | ✅ Complete | Mobile, Tablet, Desktop |

---

**Last Updated**: November 29, 2025
