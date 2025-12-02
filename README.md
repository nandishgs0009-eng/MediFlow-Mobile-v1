# 🏥 MediFlow - Healthcare Management App

A comprehensive mobile and web application for managing medical treatments, medicines, and health records. Built with React, TypeScript, and Capacitor for cross-platform support.

## ✨ Features

- 📱 **Responsive Web App** - Works on desktop and mobile browsers
- 🤖 **Native Mobile Apps** - iOS and Android support via Capacitor
- 🔐 **Secure Authentication** - Supabase integration with email/password auth
- 💊 **Treatment Management** - Create and manage treatment plans
- 💉 **Medicine Tracking** - Track medicines, dosages, and schedules
- 📊 **Health Dashboard** - View health statistics and progress
- 🔔 **Notifications** - Medicine reminders and alerts
- 📋 **Medical Records** - Store and access medical documents
- 🏃 **Recovery Reports** - Track recovery progress

## 🚀 Quick Start

### For Web Development

```bash
# Clone repository
git clone https://github.com/nandishgs0009-eng/MediFlow-Mobile-v1.git
cd MediFlow-Mobile-v1

# Install dependencies
npm install --legacy-peer-deps

# Start development server
npm run dev

# Build for production
npm run build
```

### For Mobile Development

```bash
# Setup mobile platforms
npm install --legacy-peer-deps
npm run build
npm run mobile:sync

# Open Android or iOS IDE
npm run mobile:open:android    # For Android
npm run mobile:open:ios        # For iOS (Mac only)
```

## 📱 Installation Guide

See [INSTALLATION_GUIDE.md](./INSTALLATION_GUIDE.md) for detailed instructions on:
- Setting up Android development environment
- Setting up iOS development environment
- Building and running on emulators
- Installing on physical devices
- Troubleshooting common issues

## 📚 Mobile Setup

See [MOBILE_SETUP.md](./MOBILE_SETUP.md) for:
- Available Capacitor plugins
- Development workflow
- Building for release
- App configuration
- Pro tips and best practices

## 🛠️ Available Scripts

```bash
# Web development
npm run dev                    # Start dev server
npm run build                  # Build for production
npm run build:dev             # Build in dev mode
npm run lint                  # Check code quality
npm run preview               # Preview production build

# Mobile development
npm run mobile:sync           # Sync to both platforms
npm run mobile:sync:android   # Sync to Android
npm run mobile:sync:ios       # Sync to iOS
npm run mobile:open:android   # Open Android Studio
npm run mobile:open:ios       # Open Xcode
npm run mobile:build          # Build both platforms
```

## 🏗️ Tech Stack

- **Frontend**: React 18, TypeScript, Vite
- **UI Components**: shadcn/ui, Radix UI
- **Styling**: Tailwind CSS
- **Backend**: Supabase (PostgreSQL)
- **Mobile**: Capacitor
- **State Management**: React Context, React Query
- **Forms**: React Hook Form, Zod
- **Charts**: Recharts
- **Icons**: Lucide React

## 📁 Project Structure

```
MediFlow-Mobile-v1/
├── src/
│   ├── components/          # Reusable UI components
│   ├── pages/               # Page components
│   ├── contexts/            # React contexts
│   ├── hooks/               # Custom hooks
│   ├── utils/               # Utility functions
│   └── integrations/        # Supabase integration
├── android/                 # Android native project
├── ios/                     # iOS native project
├── capacitor.config.ts     # Capacitor config
├── package.json             # Dependencies
└── README.md                # This file
```

## 🔑 Key Files

- `src/utils/capacitor-init.ts` - Mobile app initialization
- `src/utils/platform.ts` - Platform detection utilities
- `capacitor.config.ts` - Capacitor configuration
- `INSTALLATION_GUIDE.md` - Complete installation steps
- `MOBILE_SETUP.md` - Mobile development details

## 🔐 Environment Setup

Create a `.env.local` file with your Supabase credentials:

```env
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

## 📱 Platform Support

- ✅ **Web**: All modern browsers (Chrome, Firefox, Safari, Edge)
- ✅ **Android**: API 21+ (Android 5.0+)
- ✅ **iOS**: iOS 12+

## 🚦 Getting Help

- **Installation Issues**: See [INSTALLATION_GUIDE.md](./INSTALLATION_GUIDE.md)
- **Mobile Setup**: See [MOBILE_SETUP.md](./MOBILE_SETUP.md)
- **Capacitor Docs**: https://capacitorjs.com/docs
- **GitHub Issues**: https://github.com/nandishgs0009-eng/MediFlow-Mobile-v1/issues

## 📝 Development Tips

1. **Test on mobile**: Always test on actual devices before release
2. **Use DevTools**: Inspect elements in web view for debugging
3. **Check logs**: Use Android Studio logcat or Xcode console
4. **Stay updated**: Run `npx cap update` regularly

## 🔄 Workflow

1. Make changes in React components
2. Test on web: `npm run dev`
3. Build web app: `npm run build`
4. Sync to mobile: `npm run mobile:sync`
5. Test on mobile: Open Android Studio or Xcode

## 📄 License

This project is licensed under the MIT License.

## 👨‍💻 Author

Created and maintained by the MediFlow team.

---

**Ready to build? Start with the [INSTALLATION_GUIDE.md](./INSTALLATION_GUIDE.md)!** 🚀

# Step 3: Install the necessary dependencies.
npm i

# Step 4: Start the development server with auto-reloading and an instant preview.
npm run dev
```

**Edit a file directly in GitHub**

- Navigate to the desired file(s).
- Click the "Edit" button (pencil icon) at the top right of the file view.
- Make your changes and commit the changes.

**Use GitHub Codespaces**

- Navigate to the main page of your repository.
- Click on the "Code" button (green button) near the top right.
- Select the "Codespaces" tab.
- Click on "New codespace" to launch a new Codespace environment.
- Edit files directly within the Codespace and commit and push your changes once you're done.

## What technologies are used for this project?

This project is built with:

- Vite
- TypeScript
- React
- shadcn-ui
- Tailwind CSS

## How can I deploy this project?

Simply open [Lovable](https://lovable.dev/projects/eb1bb899-fd34-4660-a08b-5793bf692301) and click on Share -> Publish.

## Can I connect a custom domain to my Lovable project?

Yes, you can!

To connect a domain, navigate to Project > Settings > Domains and click Connect Domain.

Read more here: [Setting up a custom domain](https://docs.lovable.dev/features/custom-domain#custom-domain)
