# ProGen AI - Professional Illustration Generator

## 🎯 Project Overview

**ProGen AI** is an innovative web-based AI-powered platform designed to revolutionize the way businesses and creators generate professional illustrations, marketing materials, and visual content. Built as part of the TRAN4076 course project, ProGen AI leverages modern web technologies to provide a seamless user experience, including user authentication, credit-based AI generation, support ticketing, and an admin dashboard for management.

Our mission is to democratize AI-driven design tools, making high-quality illustrations accessible to small businesses, marketers, and freelancers without requiring advanced design skills. Users complete a questionnaire about their brand and products, then use accumulated credits to generate custom visuals powered by integrated AI APIs.

This project demonstrates full-stack web development principles, from frontend UI/UX to backend-like local storage management, all deployed as a static GitHub Pages site for easy accessibility.

Live Demo: [https://ivycmy4704.github.io/TRAN4076grp4.github.io/](https://ivycmy4704.github.io/TRAN4076grp4.github.io/)

## 🚀 Features

### User-Facing Features
- **User Registration & Authentication**: Secure login/register system with password recovery.
- **Credit System**: Users purchase or earn credits to generate AI illustrations (integrated with a mock payment/add-credit page).
- **Brand Questionnaire**: Interactive form to input company details, products, and preferences for personalized AI prompts.
- **AI Illustration Generator**: Dashboard for generating professional images based on questionnaire data (credits deducted per generation).
- **Support System**: Dedicated support dropbox for submitting tickets, with real-time admin responses visible in user tickets (future enhancement).
- **Responsive Design**: Mobile-friendly interface with smooth animations and modern UI.

### Admin Features
- **Admin Panel**: Secure login (admin/admin001) with full user management.
- **User Analytics**: Dashboard stats for total users, logins, tickets, and questionnaires.
- **Customer Management**: View/edit/delete users, adjust credits, and monitor login history.
- **Support Ticket Management**: View, reply to, close/reopen, and delete user tickets.
- **Questionnaire Viewer**: Comprehensive display of submitted brand/product data for admin review.
- **Search & Filtering**: Real-time search across users and tickets.

### Technical Highlights
- **Local Storage Persistence**: All data (users, tickets, questionnaires) stored client-side for offline functionality.
- **No Backend Required**: Pure frontend app using HTML5, CSS3, and vanilla JavaScript.
- **Security**: Session-based admin auth via sessionStorage; input validation on forms.

## 🛠️ Tech Stack

| Category       | Technologies/Tools |
|----------------|--------------------|
| **Frontend**   | HTML5, CSS3 (with custom gradients and animations), Vanilla JavaScript |
| **Styling**    | Custom CSS (style.css) inspired by modern admin panels (gradients, shadows, hover effects) |
| **Data Storage**| Browser LocalStorage & SessionStorage |
| **Deployment** | GitHub Pages (static hosting) |
| **AI Integration** | Placeholder for AI APIs (e.g., Stable Diffusion or DALL-E via external services; credits system simulates usage) |
| **Icons/Fonts**| Font Awesome for icons; Segoe UI for typography |
| **Other**      | Responsive design with media queries; Form validation with HTML5 attributes |

## 📁 Project Structure

```
TRAN4076grp4.github.io/
├── index.html              # Main login page
├── register.html           # User registration
├── forgot-password.html    # Password recovery (placeholder)
├── dashboard.html          # User dashboard for generations
├── credit.html             # Add credits/purchase page
├── support.html            # Support ticket submission
├── admin.html              # Admin panel (full management)
├── questionnaire.html      # Brand/product questionnaire form
├── css/
│   └── style.css           # Unified styling (admin-inspired design)
└── js/                     # (Optional: Any modular JS files)
    └── app.js              # Core logic (if separated)
```

## 📋 Installation & Setup

Since this is a **static web app**, no server setup is needed! Just host it anywhere (GitHub Pages, Netlify, Vercel).

### Local Development
1. **Clone the Repo**:
   ```
   git clone https://github.com/ivycmy4704/TRAN4076grp4.github.io.git
   cd TRAN4076grp4.github.io
   ```

2. **Open in Browser**:
   - Simply double-click `index.html` to open in your browser.
   - Or use a local server: `npx http-server` (install via npm if needed).

3. **Test Admin Access**:
   - Navigate to [admin.html](admin.html).
   - Login: Username `admin`, Password `admin001`.

4. **Clear Data (for Testing)**:
   - Open browser DevTools (F12) > Application > Local Storage > Clear all.

### Deployment to GitHub Pages
1. Push to `main` branch of `ivycmy4704/TRAN4076grp4.github.io`.
2. Enable GitHub Pages in repo settings (Source: Deploy from a branch > main > /root).
3. Access at `https://ivycmy4704.github.io/TRAN4076grp4.github.io/`.

## 📖 Usage Guide

### For Users
1. **Sign Up/Login**: Visit the homepage and create an account.
2. **Complete Questionnaire**: From dashboard, fill out your brand details (company, products, preferences).
3. **Generate Illustrations**: Use credits to create AI images based on your profile.
4. **Get Support**: Submit tickets via the Support page; check dashboard for replies.

### For Admins
1. **Login**: Go to Admin Login link > Enter credentials.
2. **Manage Users**: View/edit credits, delete accounts, monitor logins.
3. **Review Questionnaires**: Access full submitted data for client insights.


## 🔮 Future Enhancements
- **Real AI Backend**: Integrate actual APIs (e.g., OpenAI DALL-E) for image generation.
- **User Tickets**: For admins to reply to clients' tickets.
- **Payments**: Stripe integration for real credit purchases.
- **Analytics**: Chart.js for advanced dashboard visualizations.
- **Multi-Language**: i18n support for global users.
- **Export Data**: CSV download for admin reports.

---

*Built with ❤️ by Group 4 – Let's generate the future of design!*
*Generated by Grok*
