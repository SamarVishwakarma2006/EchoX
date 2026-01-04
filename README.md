# EchoX - Anonymous Student Network

EchoX is a privacy-first, college-exclusive platform that allows students to discuss exams, placements, and campus life anonymously. The platform features AI-powered moderation, file attachments, and real-time updates.

## ✨ Features

- 🔒 **100% Anonymous** - Random aliases for every interaction
- 🛡️ **AI Moderation** - Powered by Perspective API to ensure safe, respectful conversations
- 📎 **File Attachments** - Share PDFs and images (up to 50MB)
- 🏫 **College-Exclusive** - Restricted to `.edu`, `.ac.in`, `.ac.uk`, and other educational domains
- ⚡ **Real-Time Updates** - Live feed using Firebase Firestore
- 💬 **Interactive Posts** - Upvote, comment, and engage with posts
- 📱 **Responsive Design** - Works seamlessly on desktop and mobile

## 🚀 Quick Start

### Prerequisites

- A Google account with access to Firebase
- Firebase project (or create one at [Firebase Console](https://console.firebase.google.com/))
- Node.js (for Firebase CLI)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/SamarVishwakarma2006/colege-app.git
   cd colege-app
   ```

2. **Login to Firebase**
   ```bash
   firebase login
   ```
   This will open a browser window for authentication.

3. **Set Firebase Project**
   ```bash
   firebase use --add
   ```
   Select or create the `askhelp-e9fe2` project.

4. **Deploy to Firebase Hosting**
   ```bash
   firebase deploy --only hosting
   ```

Your app will be live at:
- **Primary**: `https://askhelp-e9fe2.web.app`
- **Secondary**: `https://askhelp-e9fe2.firebaseapp.com`

## 📁 Project Structure

```
colege-app/
├── clone_2/              # Main application directory
│   ├── index.html        # Single-page React application
│   ├── DEPLOYMENT_GUIDE.md
│   └── firebase.json     # (Reference config)
├── firebase.json         # Firebase hosting configuration
├── .firebaserc          # Firebase project configuration
└── README.md            # This file
```

## 🔧 Configuration

### Firebase Setup

The app uses Firebase for:
- **Authentication** - Email/password login (college emails only)
- **Firestore Database** - Store posts, comments, and user data
- **Hosting** - Deploy the web application

### Firestore Security Rules

Before deploying, ensure your Firestore Security Rules are configured:

1. Go to [Firebase Console → Firestore Rules](https://console.firebase.google.com/project/askhelp-e9fe2/firestore/rules)
2. Update rules to:
   ```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /posts/{postId} {
         allow read: if request.auth != null;
         allow create: if request.auth != null;
         allow update, delete: if request.auth != null && 
           request.auth.uid == resource.data.authorUid;
       }
     }
   }
   ```

### Environment Configuration

The Firebase configuration is embedded in `clone_2/index.html`. The project uses:
- **Project ID**: `askhelp-e9fe2`
- **API Key**: Configured in the HTML file
- **Auth Domain**: `askhelp-e9fe2.firebaseapp.com`

## 🛠️ Development

### Local Development

To run the app locally:

1. Open `clone_2/index.html` in a web browser
2. Or use a local server:
   ```bash
   # Using Python
   python -m http.server 8000
   
   # Using Node.js (http-server)
   npx http-server clone_2
   ```

### Tech Stack

- **Frontend**: React 18 (via CDN)
- **Styling**: Tailwind CSS
- **Backend**: Firebase (Firestore, Authentication)
- **Icons**: Phosphor Icons
- **Moderation**: Google Perspective API
- **Build**: No build step required (single HTML file with Babel standalone)

## 📝 Deployment

### Firebase Hosting (Recommended)

The project is already configured for Firebase Hosting. The `firebase.json` file points to the `clone_2` directory as the public folder.

```bash
# Deploy
firebase deploy --only hosting

# Deploy to specific project
firebase deploy --only hosting --project askhelp-e9fe2
```

### Alternative Deployment Options

See `clone_2/DEPLOYMENT_GUIDE.md` for detailed instructions on:
- Netlify
- Vercel
- GitHub Pages

## 🔒 Security & Privacy

- **Authentication Required**: Only authenticated users with valid college email domains can access
- **Anonymous Aliases**: User identities are hidden with randomly generated aliases
- **Content Moderation**: AI-powered toxicity detection prevents harmful content
- **Secure Rules**: Firestore security rules ensure users can only delete their own posts

## 📋 After Deployment Checklist

- [ ] Test authentication (signup/login)
- [ ] Verify college domain restrictions work
- [ ] Test creating a post
- [ ] Test file attachments
- [ ] Verify AI moderation is working
- [ ] Check Firestore Security Rules
- [ ] Test upvoting and commenting
- [ ] (Optional) Set up custom domain

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is open source and available under the MIT License.

## 🆘 Support

For issues or questions:
1. Check the [Deployment Guide](clone_2/DEPLOYMENT_GUIDE.md)
2. Open an issue on GitHub
3. Check Firebase Console for project status

## 🎯 Live URL

After deployment, your app will be available at:
- **https://askhelp-e9fe2.web.app**
- **https://askhelp-e9fe2.firebaseapp.com**

---

Built with ❤️ for students, by students.
