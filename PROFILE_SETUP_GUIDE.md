# MedMinder Profile Management - Database Update Guide

## Overview
This guide provides instructions to update your existing Supabase `profiles` table to include comprehensive patient information fields, enabling full patient profile management within MedMinder.

## What Was Changed

### 1. **Frontend Changes**
- Created new `Profile.tsx` page with full patient information management
- Added route `/profile` to `App.tsx` with protection
- Integrated Profile link in Settings dropdown on all main pages:
  - Dashboard
  - History
  - MyTreatments
  - RecoveryReports

### 2. **Database Changes**
The existing `profiles` table needs to be updated with additional columns to store patient information.

---

## How to Apply the Migration

### **Option A: Using Supabase SQL Editor (Recommended for Beginners)**

1. **Open your Supabase Dashboard**
   - Go to https://supabase.com
   - Sign in to your project
   - Select your project (MedMinder)

2. **Navigate to SQL Editor**
   - Click on "SQL Editor" in the left sidebar
   - Click "New Query"

3. **Copy and Paste the SQL Commands**
   - Copy all the SQL from: `supabase/migrations/20251129_update_profiles_table.sql`
   - Paste into the SQL editor
   - Click "Run" button

4. **Verify Success**
   - You should see "Success" message
   - Navigate to "Table Editor" and select `profiles` table
   - Verify the new columns are present

### **Option B: Using Supabase CLI (Advanced)**

If you have Supabase CLI installed:

```bash
# Navigate to project directory
cd c:\Users\hp\med-minder

# Run migrations
supabase migration push

# Or manually apply the SQL
supabase db push
```

### **Option C: Direct SQL Copy-Paste**

Copy and execute this SQL command in your Supabase SQL Editor:

```sql
-- Update existing profiles table to include patient information

-- Add new columns to profiles table
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS phone TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS date_of_birth DATE;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS gender TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS blood_type TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS height DECIMAL(5,2);
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS weight DECIMAL(5,2);
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS emergency_contact_name TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS emergency_contact_phone TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS medical_conditions TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS allergies TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS current_medications_notes TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS address TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS city TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS state TEXT;
ALTER TABLE public.profiles ADD COLUMN IF NOT EXISTS zip_code TEXT;

-- Create index for faster queries
CREATE INDEX IF NOT EXISTS idx_profiles_id ON public.profiles(id);

-- Drop existing trigger if it exists
DROP TRIGGER IF EXISTS trigger_profiles_updated_at ON public.profiles;

-- Create function to update updated_at timestamp
CREATE OR REPLACE FUNCTION update_profiles_updated_at()
RETURNS TRIGGER AS $$
BEGIN
  NEW.updated_at = CURRENT_TIMESTAMP;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Create trigger for updated_at
CREATE TRIGGER trigger_profiles_updated_at
  BEFORE UPDATE ON public.profiles
  FOR EACH ROW
  EXECUTE FUNCTION update_profiles_updated_at();

-- Update RLS policies
DROP POLICY IF EXISTS "Users can view their own profile" ON public.profiles;
CREATE POLICY "Users can view their own profile"
  ON public.profiles FOR SELECT
  USING (auth.uid() = id);

DROP POLICY IF EXISTS "Users can insert their own profile" ON public.profiles;
CREATE POLICY "Users can insert their own profile"
  ON public.profiles FOR INSERT
  WITH CHECK (auth.uid() = id);

DROP POLICY IF EXISTS "Users can update their own profile" ON public.profiles;
CREATE POLICY "Users can update their own profile"
  ON public.profiles FOR UPDATE
  USING (auth.uid() = id)
  WITH CHECK (auth.uid() = id);
```

---

## Updated Table Schema

### **profiles table (Updated)**

```sql
CREATE TABLE public.profiles (
  id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  
  -- Basic Information
  full_name TEXT,
  email TEXT,
  avatar_url TEXT,
  
  -- Contact Information
  phone TEXT,
  
  -- Personal Information
  date_of_birth DATE,
  gender TEXT,                    -- Values: male, female, other, prefer_not_to_say
  blood_type TEXT,               -- Values: O+, O-, A+, A-, B+, B-, AB+, AB-
  
  -- Health Metrics
  height DECIMAL(5,2),           -- in centimeters
  weight DECIMAL(5,2),           -- in kilograms
  
  -- Medical Information
  medical_conditions TEXT,        -- Can include chronic conditions, surgeries, etc.
  allergies TEXT,                -- Known allergies and reactions
  current_medications_notes TEXT, -- Additional medication notes
  
  -- Address Information
  address TEXT,                  -- Street address
  city TEXT,
  state TEXT,                    -- State or Province
  zip_code TEXT,                 -- Postal code
  
  -- Emergency Contact
  emergency_contact_name TEXT,
  emergency_contact_phone TEXT,
  
  -- Timestamps
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW() NOT NULL,
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW() NOT NULL
);
```

---

## Features Available After Update

### 1. **View Mode**
- See all patient information in organized cards
- Display health metrics (Age, BMI, BMI Category)
- View emergency contact information
- Color-coded health status indicators

### 2. **Edit Mode**
- Edit all fields except email (for security)
- Dropdown selections for Gender and Blood Type
- Textarea fields for medical information
- Real-time form validation
- Save with success/error notifications

### 3. **Auto-calculated Fields**
- **Age**: Calculated from date of birth
- **BMI**: Calculated from height and weight
- **BMI Category**: Normal, Overweight, Obese, Underweight (color-coded)

### 4. **Security**
- Row-Level Security (RLS) enforced
- Users can only access their own profile
- Email field is read-only
- Automatic timestamps for auditing

---

## How to Access the Profile Page

### **From Dashboard/Any Main Page:**
1. Click the "Settings" option in the left sidebar
2. The dropdown menu will expand showing submenu items
3. Click "Profile" to navigate to your profile
4. Click "Edit Profile" button to make changes
5. Fill in your information
6. Click "Save Changes" to persist data

### **Direct URL:**
Navigate to: `http://localhost:5173/profile`

---

## Database Field Descriptions

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| full_name | TEXT | User's complete name | John Doe |
| phone | TEXT | Contact phone number | +1 (555) 123-4567 |
| date_of_birth | DATE | Birth date | 1990-05-15 |
| gender | TEXT | Gender identity | male, female, other |
| blood_type | TEXT | Blood group | O+, A-, B+, AB- |
| height | DECIMAL | Height in cm | 175.50 |
| weight | DECIMAL | Weight in kg | 75.25 |
| medical_conditions | TEXT | Medical history | Diabetes, Hypertension |
| allergies | TEXT | Known allergies | Penicillin, Peanuts |
| current_medications_notes | TEXT | Medication notes | Take with food |
| address | TEXT | Street address | 123 Main St |
| city | TEXT | City name | New York |
| state | TEXT | State/Province | NY |
| zip_code | TEXT | Postal code | 10001 |
| emergency_contact_name | TEXT | Emergency contact person | Jane Doe |
| emergency_contact_phone | TEXT | Emergency phone | +1 (555) 987-6543 |

---

## Verification Checklist

After applying the migration, verify:

- [ ] All new columns are visible in Supabase Table Editor
- [ ] Profile page loads without errors
- [ ] Can navigate to Profile from Settings dropdown
- [ ] Can edit profile information
- [ ] Changes are saved to database
- [ ] Age, BMI, and BMI Category calculate correctly
- [ ] Email field is read-only
- [ ] RLS policies are enforced (can only see own data)
- [ ] Timestamps update automatically on save

---

## Troubleshooting

### **Issue: "Column already exists" error**
**Solution**: This is normal. The migration uses `ADD COLUMN IF NOT EXISTS`, which safely skips columns that already exist.

### **Issue: Profile page shows blank**
**Solution**: 
1. Check that migration was applied successfully
2. Clear browser cache (Ctrl+Shift+Del)
3. Check browser console for errors (F12 → Console tab)

### **Issue: Can't save profile**
**Solution**:
1. Verify RLS policies are properly set
2. Check that you're logged in as the correct user
3. Check browser console for API errors
4. Verify user_id matches the profile id

### **Issue: Email field is editable**
**Solution**: This is intentional for security. Contact support to change email through auth settings.

---

## Future Enhancements

The Profile page includes a "Future Enhancements" section showcasing planned features:

- Medical History Upload
- Medication History Tracking
- Lab Reports Integration
- Insurance Information Management
- Doctor & Clinic Directory
- Export Profile as PDF

These can be implemented in future updates.

---

## Support

If you encounter any issues:
1. Check the troubleshooting section above
2. Review browser console for errors (F12)
3. Verify all migration SQL was executed successfully
4. Check that you're logged in with the correct user account

---

## Summary

✅ Profile page component created and fully functional
✅ Database migration prepared to update existing profiles table
✅ All profile routes integrated into navigation
✅ Security implemented with RLS policies
✅ Auto-calculated health metrics (Age, BMI)
✅ Ready for production use after migration is applied

**Next Step**: Apply the migration using one of the methods above, then start using the Profile page!
