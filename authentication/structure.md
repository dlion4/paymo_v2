PAYMO BAAS — ADVANCED AUTHENTICATION & ACCOUNT SELECTION ARCHITECTURE
Multi-Factor Auth, Account Type Selection & Dashboard Routing System
Document Version: 1.4
571 9529
hira til number till oscra 
Date: June 2026
Classification: Strategic IA / Authentication & User Onboarding Architecture
________________________________________
TABLE OF CONTENTS
•	Overview & Authentication Philosophy
•	Page 51: Authentication Gateway / Login Hub
•	Page 52: Create Account / Registration Flow
•	Page 53: Forgot Password / PIN Recovery
•	Page 54: Multi-Factor Authentication (MFA) Challenge
•	Page 55: Account Status (account recovery, verify details, verify bank account, despute transaction etc)   Selection (Post-Login)
•	Page 56: Dashboard Selection Hub
•	Page 57: Session Management & Security Center
•	Page 58: Biometric Setup & Passkey Management
•	Page 59: Account Recovery & Identity Verification
•	Page 60: Login Activity & Fraud Alerts
________________________________________
 ## OVERVIEW & AUTHENTICATION PHILOSOPHY
Core Principles
1.	Frictionless Security — Security that enhances, not hinders, the user experience.
2.	Progressive Authentication — Escalate authentication requirements based on risk, not one-size-fits-all.
3.	User Choice — Multiple authentication methods, user selects preferred primary method.
4.	Zero-Trust by Default — Verify every session, every device, every transaction context.
5.	Accessibility First — Authentication must work for users with disabilities, low connectivity, and basic devices.
Authentication Methods Supported
Method	Security Level	UX Friction	Use Case
Passkey (FIDO2/WebAuthn)	Very High	Very Low	Primary method for supported devices
Password + 2FA	High	Medium	Legacy fallback, high-risk transactions
PIN (6-digit)	Medium	Low	Mobile app, quick access, low-risk contexts
Biometric (Face/Touch)	High	Very Low	Mobile native, seamless experience
Social Login (Google, Apple, etc.)	Medium	Very Low	Speed onboarding, social proof
Magic Link (Email)	Medium	Low	Passwordless, email-verified
OTP (SMS/WhatsApp/Email)	Medium	Medium	2FA factor, recovery, device binding
Hardware Security Key	Very High	Low	Enterprise, high-value accounts
Pattern/Draw	Low	Very Low	Quick mobile unlock (optional)
Risk-Based Authentication Triggers
•	New device or browser fingerprint.
•	Unusual geolocation (impossible travel detection).
•	Time-of-day anomaly (login at 3 AM when user never does).
•	IP reputation (VPN, Tor, known malicious IP).
•	Velocity (multiple failed attempts).
•	Transaction amount threshold (>$10K requires step-up auth).
•	Sensitive action (changing password, adding beneficiary, API key rotation).
________________________________________
 ## PAGE 51: AUTHENTICATION GATEWAY / LOGIN HUB URL: /auth/login
Goal: Universal entry point with multiple authentication pathways.
Audience: All returning users.
Section 51.1 — Dynamic Hero / Brand Lockup
•	Visual: Clean, minimal layout with Paymo logo centered. Subtle animated gradient background (deep forest green to charcoal). No distractions — focus entirely on authentication.
•	Headline: “Welcome Back” (personalized if returning user detected: “Welcome back, [First Name]”).
•	Subheadline: “Sign in to your Paymo account securely.”
•	Contextual Banner: If user was redirected from a protected route: “Please sign in to access [Dashboard/Feature].”
•	Security Badge: “🔒 Secured by Paymo Shield — 256-bit encryption” with tooltip explaining security measures.
Section 51.2 — Primary Authentication Method Selector (Tabs)
•	Visual: Horizontal tab bar with icons, defaulting to user’s last used method (stored in localStorage with consent).
•	Tab 1 — Passkey (Recommended)
–	Icon: Fingerprint/Security key icon.
–	Label: “Use Passkey” with “Fastest & Most Secure” badge.
–	Active State: Browser-native WebAuthn prompt triggers automatically on page load (if passkey registered).
–	Button: “Sign in with Passkey” — triggers platform authenticator (Face ID, Touch ID, Windows Hello, Android Biometric).
–	Fallback: “Don’t have a passkey? Set one up after login.”
–	Device Compatibility Check: Auto-detect if device supports passkeys; if not, tab is disabled with tooltip.
•	Tab 2 — Password
–	Icon: Lock icon.
–	Email/Phone Input: Auto-complete enabled, validates format in real-time.
–	Password Input: Toggle visibility (eye icon), strength indicator on registration (not login), paste allowed.
–	Remember Me: Checkbox, 30-day persistent session (encrypted cookie).
–	Sign In Button: Primary CTA, loading state with spinner, disabled until valid input.
–	Auto-redirect: If user has 2FA enabled, redirect to MFA challenge page after password validation.
•	Tab 3 — PIN (Mobile-Optimized)
–	Icon: Keypad icon.
–	6-Digit PIN Input: Large touch-friendly circles, numeric keyboard on mobile, auto-advance per digit.
–	Visual Feedback: Dots fill as digits entered, shake animation on error.
–	Biometric Override: “Or use Face ID/Touch ID” button (if biometric enrolled).
–	Use Case: Primarily for mobile app login, quick dashboard access.
•	Tab 4 — Magic Link (Passwordless)
–	Icon: Link/Wand icon.
–	Email Input: “Enter your email and we’ll send you a secure login link.”
–	Send Button: Triggers email dispatch, shows countdown (“Link sent! Check your inbox. Resend in 60s”).
–	Email Content Preview: Shows what the email looks like (prevents phishing confusion).
–	Expiry: Link valid for 15 minutes, single-use.
•	Tab 5 — Social Login
–	Icon: Social media icons.
–	Buttons:
•	“Continue with Google” (OAuth 2.0, Google Identity Services).
•	“Continue with Apple” (Sign in with Apple, private relay email option).
•	“Continue with Microsoft” (Azure AD, enterprise SSO).
•	“Continue with LinkedIn” (professional verification).
–	Privacy Note: “We only access your name, email, and profile photo. We never post on your behalf.”
–	Account Linking: If social email matches existing account, auto-link after confirmation.
Section 51.3 — Contextual Smart Defaults
•	Visual: Auto-detected method highlighted.
•	Logic:
–	If user last logged in with passkey → auto-trigger passkey prompt.
–	If on mobile app → default to PIN/biometric tab.
–	If on desktop + enterprise domain → default to SSO/Microsoft.
–	If new device detected → show all options, recommend passkey setup.
•	Device Fingerprint Display: “You’re signing in from Chrome on Windows in Lagos, Nigeria” (helps user detect unauthorized access).
Section 51.4 — Security Features Strip
•	Visual: Horizontal icon strip below login form.
•	End-to-End Encryption: “Your credentials are encrypted in transit and at rest.”
•	Fraud Monitoring: “Unusual login attempts are blocked automatically.”
•	No Password Storage: “We use zero-knowledge architecture for maximum security.”
•	Compliance: “PCI DSS Level 1 • SOC 2 Type II • ISO 27001”
Section 51.5 — Auxiliary Actions
•	Visual: Clean link row.
•	Create Account: “New to Paymo? Create an account” → /auth/register
•	Forgot Password/PIN: “Forgot your password or PIN?” → /auth/recovery
•	Help: “Need help signing in?” → Opens chatbot or /help/auth-issues
•	Switch Account: “Sign in to a different account” (clears remembered user).
Section 51.6 — Footer
•	Visual: Minimal footer.
•	Links: Privacy Policy | Terms of Use | Cookie Settings | Accessibility
•	Language Selector: 8 languages.
•	Copyright: © 2026 Paymo Financial Technologies Ltd.
________________________________________
 ## PAGE 52: CREATE ACCOUNT / REGISTRATION FLOW URL: /auth/register
Goal: Convert visitors to registered users with minimal friction, maximum security setup.
Audience: New users — individuals, business owners, developers.
Section 52.1 — Registration Gateway
•	Visual: Split screen — left side brand imagery (diverse Africans using financial services), right side registration form.
•	Headline: “Join Paymo — Your Financial World, Unified.”
•	Subheadline: “Create your account in 2 minutes. No paperwork, no branch visits.”
•	Trust Signals: “✓ 2M+ users | ✓ Bank-grade security | ✓ Free to join”
Section 52.2 — Account Type Selection (Step 1)
•	Visual: 3 large cards with icons and descriptions.
•	Card 1 — Personal
–	Icon: Person silhouette.
–	Title: “Personal Account”
–	Description: “Send money, pay bills, shop online, and manage your finances across Africa.”
–	Best For: Individuals, freelancers, gig workers.
–	CTA: “Get Started — Personal”
•	Card 2 — Business
–	Icon: Building/Shop icon.
–	Title: “Business Account”
–	Description: “Accept payments, pay suppliers, manage payroll, and access working capital.”
–	Best For: SMEs, retailers, e-commerce, service providers.
–	CTA: “Get Started — Business”
–	Badge: “Free business account setup”
•	Card 3 — Developer / Fintech
–	Icon: Code brackets icon.
–	Title: “Developer Account”
–	Description: “Build financial products with our APIs. Sandbox access, documentation, and community.”
–	Best For: Developers, fintech founders, neobank builders.
–	CTA: “Get Started — Developer”
–	Badge: “Free API credits included”
•	Selection Logic: Clicking a card expands the relevant registration form without page reload (SPA behavior).
Section 52.3 — Personal Account Registration (Step 2A)
•	Visual: Multi-step progress bar (Step 1 of 3: Basic Info → Identity → Security).
•	Step 2A.1 — Basic Information:
–	Full Name (first, middle optional, last).
–	Email Address (real-time validation, MX record check).
–	Phone Number (country selector with flag, auto-formatting, SMS verification trigger).
–	Date of Birth (date picker, age validation 18+).
–	Country of Residence (dropdown with 25+ African + global markets).
–	Referral Code (optional).
•	Step 2A.2 — Identity Verification (KYC):
–	Document Type selector (Passport, National ID, Driver’s License, Voter’s Card — country-specific options).
–	Document Upload: Drag-and-drop with real-time quality check (glare, blur, cropping guidance).
–	Selfie Capture: In-browser camera with liveness detection (blink, turn head).
–	Auto-Verification: “Verifying…” animation, typically completes in <30 seconds.
–	Manual Review Fallback: “We’re reviewing your documents. This usually takes 2–4 hours.”
•	Step 2A.3 — Security Setup:
–	Create Password (strength meter: Weak/Fair/Strong/Very Strong, requirements displayed).
–	Confirm Password.
–	Set 6-Digit PIN (for mobile app quick access).
–	Confirm PIN.
–	Passkey Setup Prompt: “Want faster, more secure logins? Set up a passkey now.” (Optional, skippable).
–	Biometric Enrollment (if on mobile): “Enable Face ID/Touch ID for instant access?”
–	Security Questions (3 questions, selectable from pool of 15 — used for account recovery).
•	Step 2A.4 — Consent & Terms:
–	Checkbox: “I agree to the Terms of Use and Privacy Policy” (links open in modal).
–	Checkbox: “I consent to receiving marketing communications” (optional, unchecked by default).
–	Checkbox: “I confirm I am 18 years or older.”
–	ReCAPTCHA v3 (invisible, no user friction).
–	“Create Account” button (disabled until all required fields valid and terms accepted).
Section 52.4 — Business Account Registration (Step 2B)
•	Visual: Progress bar (Step 1 of 4: Business Info → KYB → Representative → Security).
•	Step 2B.1 — Business Information:
–	Business Name (trading name + registered name if different).
–	Business Type (Sole Proprietorship, Partnership, LLC, PLC, NGO, Cooperative).
–	Industry Category (dropdown with 50+ options).
–	Registration Number (auto-validated against corporate registry where API available).
–	Tax ID / VAT Number.
–	Business Address (street, city, state, postal code, country).
–	Website (optional, URL validation).
–	Estimated Monthly Volume (ranges: <$1K, $1K–$10K, $10K–$100K, $100K–$1M, $1M+).
•	Step 2B.2 — Know Your Business (KYB):
–	Certificate of Incorporation upload.
–	Memorandum & Articles of Association upload.
–	Business Bank Statement (last 3 months, for verification).
–	Proof of Business Address (utility bill, lease agreement).
•	Step 2B.3 — Authorized Representative:
–	Same as Personal KYC (Step 2A.2) for business owner/director.
–	UBO Declaration (Ultimate Beneficial Owners — name, % ownership, ID verification for each 25%+ owner).
–	Director details (name, position, ID verification).
•	Step 2B.4 — Security Setup:
–	Same as Personal (Step 2A.3).
–	Additional: Admin user setup (primary admin + optional secondary admin).
–	Role permissions preview (Owner, Admin, Finance, Viewer).
Section 52.5 — Developer Account Registration (Step 2C)
•	Visual: Progress bar (Step 1 of 3: Profile → Verification → API Setup).
•	Step 2C.1 — Developer Profile:
–	Same basic info as Personal (name, email, phone).
–	Company/Organization (if applicable, links to Business account if exists).
–	GitHub Profile (optional, for community recognition).
–	Primary Use Case (dropdown: Neobank, E-commerce, Remittance, Lending, Other).
–	Expected API Volume (ranges).
–	Programming Languages (multi-select: Node.js, Python, Go, PHP, Ruby, Java, .NET, Flutter, iOS, Android).
•	Step 2C.2 — Identity Verification:
–	Same as Personal KYC (Step 2A.2).
–	If linked to Business account, KYB satisfies requirement.
•	Step 2C.3 — API Setup:
–	Auto-generate Sandbox API Keys (displayed once, copy-to-clipboard).
–	Webhook URL input (optional, can configure later).
–	First API Call Tutorial (interactive: “Make your first API call in 30 seconds”).
–	Documentation quick links.
–	Discord community invite.
Section 52.6 — Post-Registration Success
•	Visual: Celebration animation (confetti, checkmark).
•	Headline: “Welcome to Paymo, [Name]! 🎉”
•	Personalized Next Steps:
–	Personal: “Add money to your wallet” | “Set up your first bill payment” | “Invite friends and earn”
–	Business: “Complete your profile” | “Add your first team member” | “Create a payment link”
–	Developer: “Explore the API docs” | “Join the Discord community” | “Build your first integration”
•	Email Confirmation: “We’ve sent a confirmation email to [email]. Please verify to unlock all features.”
•	CTA: “Go to Account Type Selection” → /auth/account-type
Section 52.7 — Social Registration Shortcut
•	Visual: Social login buttons at top of registration form.
•	One-Click Signup: Google, Apple, Microsoft, LinkedIn.
•	Data Pre-fill: Social profile data auto-fills registration form (editable).
•	KYC Still Required: Social login skips basic info but identity verification still mandatory for financial services.
________________________________________
 ## PAGE 53: FORGOT PASSWORD / PIN RECOVERY URL: /auth/recovery
Goal: Secure, user-friendly account recovery with multiple verification pathways.
Audience: Locked-out users, security-conscious users rotating credentials.
Section 53.1 — Recovery Gateway
•	Visual: Clean, reassuring layout (no panic-inducing red).
•	Headline: “Account Recovery”
•	Subheadline: “We’ll help you get back in securely. Choose how you’d like to recover your account.”
•	Security Note: “For your protection, recovery may take a few minutes. We appreciate your patience.”
Section 53.2 — Recovery Method Selector
•	Visual: 4 method cards, availability depends on user’s enrolled methods.
•	Method 1 — Email Reset Link
–	Icon: Envelope.
–	“Send a password reset link to your registered email.”
–	Input: Email address (pre-filled if remembered).
–	Button: “Send Reset Link”
–	Process: Link sent → 15-minute expiry → click link → set new password → auto-login.
–	Security: Link single-use, device-bound (invalid if opened on different device).
•	Method 2 — SMS/WhatsApp OTP
–	Icon: Phone/Message bubble.
–	“Receive a one-time code via SMS or WhatsApp.”
–	Input: Phone number (last 4 digits shown for verification, e.g., “+234 •••••1234”).
–	Button: “Send OTP”
–	Process: 6-digit code → 5-minute expiry → enter code → set new password/PIN.
–	WhatsApp Option: “Prefer WhatsApp?” toggle for markets where WhatsApp is dominant.
•	Method 3 — Security Questions
–	Icon: Shield/Question mark.
–	“Answer your security questions.”
–	Displays 2 of 3 enrolled questions randomly.
–	Input: Free-text answers (case-insensitive matching).
–	Attempt Limit: 3 attempts, then 24-hour lockout.
–	Post-Verification: Set new password/PIN.
•	Method 4 — Biometric / Passkey Recovery
–	Icon: Fingerprint/Key.
–	“Use your registered passkey or biometric to verify identity.”
–	Triggers WebAuthn prompt.
–	If successful: Direct access to password reset (no additional verification needed).
–	Fallback: If passkey fails, routes to alternate method.
Section 53.3 — Recovery via Trusted Device
•	Visual: Device list with verification options.
•	Content: “We noticed you’re trying to recover from a new device. You can also approve this recovery from a trusted device.”
•	Trusted Device List: Shows user’s enrolled devices (e.g., “iPhone 15 — Lagos, Nigeria — Last used 2 days ago”).
•	Push Notification: Send approval request to trusted device.
•	QR Code Scan: Scan QR with trusted device to approve recovery.
Section 53.4 — Account Recovery via Support (Last Resort)
•	Visual: Support contact card with clear escalation path.
•	Content: “If you can’t use any of the above methods, our support team can help after identity verification.”
•	Process:
–	Submit recovery request with government ID upload.
–	Video call verification (scheduled within 24 hours).
–	48-hour security hold after verification (cooling-off period).
–	Account restored with mandatory password change and 2FA re-enrollment.
•	Warning: “This process takes 3–5 business days. For faster recovery, please try the automated methods above.”
Section 53.5 — Post-Recovery Security Measures
•	Visual: Security checklist.
•	Mandatory Actions:
–	Set new strong password (cannot reuse last 5 passwords).
–	Re-enroll 2FA (if previously enabled).
–	Review and update security questions.
–	Check recent login activity for unauthorized access.
–	Revoke all active sessions (log out all devices).
•	Optional: Set up passkey for future passwordless recovery.
Section 53.6 — Fraud Prevention During Recovery
•	Visual: Subtle security indicators.
•	Rate Limiting: Max 3 recovery attempts per hour, 5 per day.
•	Device Fingerprinting: Recovery from unusual device triggers additional verification.
•	Geolocation Check: Recovery from different country triggers email alert + delayed processing.
•	Time Delay: High-risk recoveries have 24-hour cooling-off period before account restored.
________________________________________
 ## PAGE 54: MULTI-FACTOR AUTHENTICATION (MFA) CHALLENGE URL: /auth/mfa
Goal: Secure step-up authentication with multiple factor options.
Audience: Users with MFA enabled, users triggering risk-based step-up.
Section 54.1 — MFA Challenge Screen
•	Visual: Clean, focused layout with security branding.
•	Headline: “Verify Your Identity”
•	Subheadline: “We need to confirm it’s really you. Choose how you’d like to verify.”
•	Context Display: “Signing in from Chrome on Windows in Lagos, Nigeria” (helps user confirm legitimacy).
Section 54.2 — MFA Method Selector
•	Visual: Method cards with last-used indicator.
•	Method 1 — Authenticator App (TOTP)
–	Icon: Shield with clock.
–	“Enter the 6-digit code from your authenticator app (Google Authenticator, Authy, Microsoft Authenticator).”
–	Input: 6-digit code with auto-advance.
–	Timer: 30-second countdown with progress bar.
–	“Can’t access your authenticator?” → Recovery codes option.
•	Method 2 — SMS/WhatsApp OTP
–	Icon: Phone.
–	“We’ll send a code to +234 •••••1234.”
–	Button: “Send Code”
–	Input: 6-digit code, 5-minute expiry.
–	WhatsApp toggle for supported markets.
•	Method 3 — Email OTP
–	Icon: Envelope.
–	“We’ll send a code to c•••@example.com.”
–	Button: “Send Code”
–	Input: 6-digit code, 10-minute expiry.
•	Method 4 — Push Notification
–	Icon: Bell.
–	“Send a push notification to your Paymo mobile app.”
–	Button: “Send Push”
–	Display: “Check your phone — tap ‘Approve’ to continue.”
–	Timeout: 60 seconds, auto-retry once.
•	Method 5 — Biometric (Mobile App)
–	Icon: Fingerprint.
–	“Use Face ID or Touch ID on your registered device.”
–	Button: “Trigger Biometric”
–	Process: Deep link to mobile app → biometric prompt → auto-redirect back.
•	Method 6 — Hardware Security Key
–	Icon: USB key.
–	“Tap your YubiKey or other FIDO2 security key.”
–	Button: “Use Security Key”
–	Process: WebAuthn prompt → physical key touch → verified.
Section 54.3 — Recovery Codes
•	Visual: Expandable section.
•	Content: “Lost access to your authenticator? Use a recovery code.”
•	Input: One-time recovery code (8-digit alphanumeric).
•	Warning: “Each recovery code can only be used once. After use, generate new codes in Security Center.”
•	Link: “Don’t have recovery codes?” → Routes to identity verification + support.
Section 54.4 — Remember This Device
•	Visual: Checkbox with explanation.
•	Content: “Don’t ask again for 30 days on this device.”
•	Security Note: “Only check this on personal, secure devices.”
•	Smart Default: Unchecked for new devices, pre-checked for previously trusted devices.
Section 54.5 — Risk-Based Step-Up Scenarios
•	Visual: Scenario cards (educational, not shown during challenge).
•	Why am I seeing this? Contextual explanation based on trigger:
–	“You’re signing in from a new device.”
–	“Your location has changed significantly.”
–	“This is an unusually large transaction.”
–	“You haven’t signed in for 30+ days.”
–	“We’re updating our security requirements.”
Section 54.6 — Failed MFA Handling
•	Visual: Progressive escalation.
•	1st Failure: “Incorrect code. Please try again.” (3 attempts remaining).
•	2nd Failure: “Incorrect again. Make sure your device’s time is synced.” (2 attempts remaining).
•	3rd Failure: “One attempt remaining. After this, your account will be temporarily locked for 30 minutes.”
•	Lockout: Account locked, email sent with unlock instructions (identity verification required).
________________________________________
 ## PAGE 55: ACCOUNT TYPE SELECTION (POST-LOGIN) URL: /auth/account-type
Goal: Route users to appropriate dashboard based on their account type and intent.
Audience: All authenticated users immediately after login.
Section 55.1 — Welcome Back Header
•	Visual: Personalized greeting with user’s profile photo and name.
•	Headline: “Welcome back, [First Name] 👋”
•	Subheadline: “Select how you’d like to use Paymo today.”
•	Last Used Indicator: “You last used: [Account Type] — [Time Ago]” with quick-reaccess button.
Section 55.2 — Account Type Cards (Primary Selection)
•	Visual: 3 large, rich cards with hover animations and detailed previews.
•	Card 1 — Personal Account
–	Icon: Person avatar with wallet.
–	Title: “Personal”
–	Subtitle: “Manage your money, pay bills, send transfers”
–	Preview Stats: Wallet balance, recent transactions, upcoming bills.
–	Quick Actions: “Send Money” | “Pay Bills” | “View Wallet”
–	Color Accent: Teal/Green gradient.
–	Badge: “Active” (if user has personal account).
–	Animation: Card subtly pulses if user has unread notifications.
•	Card 2 — Business Account
–	Icon: Building with chart.
–	Title: “Business”
–	Subtitle: “Payments, payroll, invoices, and team management”
–	Preview Stats: Today’s collections, pending payouts, team member count.
–	Quick Actions: “Collect Payment” | “Send Payout” | “View Dashboard”
–	Color Accent: Navy/Blue gradient.
–	Badge: “Active” or “Setup Required” (if registered but incomplete).
–	Animation: Notification dot if pending approvals or failed transactions.
•	Card 3 — Developer / API
–	Icon: Code brackets with terminal.
–	Title: “Developer”
–	Subtitle: “API keys, sandbox, documentation, and integrations”
–	Preview Stats: API calls today, active webhooks, sandbox status.
–	Quick Actions: “API Dashboard” | “View Docs” | “Test Sandbox”
–	Color Accent: Purple/Violet gradient.
–	Badge: “Active” or “New” (if first visit).
–	Animation: Live API call counter ticking.
Section 55.3 — Multiple Account Management
•	Visual: Account switcher for users with multiple account types.
•	Content: “You have access to multiple account types. Switch anytime from the top navigation.”
•	Unified View Option: “View Unified Summary” — shows balances and recent activity across all account types in one view.
•	Quick Switch: Dropdown in header for instant account type switching without full page reload.
Section 55.4 — Account Setup Prompts
•	Visual: Contextual prompts for incomplete setups.
•	If Personal account incomplete: “Complete your profile to unlock all features →” (progress bar showing 70% complete).
•	If Business account pending verification: “Your business verification is in progress. Estimated completion: 4 hours.”
•	If Developer account not activated: “Activate your sandbox to start building →”
Section 55.5 — Recent Activity Preview
•	Visual: Mini activity feed below account cards.
•	Content: “Recent activity across your accounts:”
•	Items: “Personal: Sent $500 to Kenya — 2 hours ago” | “Business: Received payment from Customer XYZ — 5 hours ago” | “Developer: 1,240 API calls today”
•	CTA: “View All Activity”
Section 55.6 — Promotions & Announcements
•	Visual: Dismissible banner cards.
•	Example: “New: Pay bills in 5 countries from one dashboard. Try it now →”
•	Example: “Developer: Webhook v2 is now live with 50% faster delivery.”
•	Personalization: Based on account type and usage patterns.
Section 55.7 — CTA: “Continue to Dashboard Selection”
•	Visual: Selected account type highlights, “Continue” button activates.
•	Behavior: Clicking an account card selects it; clicking “Continue” routes to Dashboard Selection Hub (/dashboard/select) with context of chosen account type.
________________________________________
 ## PAGE 56: DASHBOARD SELECTION HUB URL: /dashboard/select
Goal: Present role-appropriate dashboards based on account type and user permissions.
Audience: Authenticated users post-account-type-selection.
Section 56.1 — Dynamic Dashboard Header
•	Visual: Context-aware header showing selected account type and user role.
•	Headline: “[Account Type] Dashboards”
•	Subheadline: “Choose your workspace. You can switch anytime.”
•	Breadcrumb: Home → Account Type → Dashboard Selection.
•	Role Badge: “Admin” | “Finance” | “Viewer” | “Developer” (based on permissions).
Section 56.2 — Personal Account Dashboards
•	Visual: 4 rich cards in 2x2 grid.
•	Card 1 — Transactions Dashboard
–	Icon: Arrows in/out.
–	Title: “My Transactions”
–	Description: “View all your payments, transfers, and receipts. Track spending patterns and download statements.”
–	Preview Metrics: “12 transactions this week | $1,240 total volume | 3 pending”
–	Key Features List:
•	Real-time transaction feed with filters (date, type, amount, status).
•	Spending analytics by category (food, transport, bills, shopping).
•	Monthly statement generation (PDF download).
•	Transaction dispute initiation.
•	Recurring transaction management.
–	Quick Actions: “Send Money” | “Request Money” | “Download Statement”
–	Color: Teal.
–	CTA: “Open Transactions”
•	Card 2 — Services & Utilities Dashboard
–	Icon: Lightning bolt + water drop.
–	Title: “Bills & Utilities”
–	Description: “Manage all your bill payments, subscriptions, and service providers in one place.”
–	Preview Metrics: “5 active billers | 2 due this week | NGN 45,000 monthly spend”
–	Key Features List:
•	Biller directory (200+ providers across 25 markets).
•	Auto-pay setup and management.
•	Bill payment history and receipts.
•	Usage analytics and budget alerts.
•	New biller request form.
–	Quick Actions: “Pay Bill” | “Add Biller” | “Set Auto-Pay”
–	Color: Blue.
–	CTA: “Open Bills & Utilities”
•	Card 3 — Wallet & Cards Dashboard
–	Icon: Wallet with cards.
–	Title: “My Wallet & Cards”
–	Description: “Manage your balances, virtual accounts, and card settings.”
–	Preview Metrics: “3 currencies active | $2,400 balance | 2 virtual cards”
–	Key Features List:
•	Multi-currency wallet management.
•	Virtual account details and transactions.
•	Virtual/physical card controls (freeze, limits, merchant blocks).
•	FX conversion with rate locking.
•	Savings goals and round-ups.
–	Quick Actions: “Add Money” | “Convert Currency” | “Order Card”
–	Color: Green.
–	CTA: “Open Wallet”
•	Card 4 — Profile & Settings Dashboard
–	Icon: Gear/Person.
–	Title: “Profile & Settings”
–	Description: “Manage your personal information, security settings, and preferences.”
–	Preview Metrics: “85% profile complete | 2FA enabled | 3 trusted devices”
–	Key Features List:
•	Personal information editing.
•	KYC document updates.
•	Security settings (password, PIN, biometrics, passkeys).
•	Notification preferences.
•	Connected apps and API tokens.
–	Quick Actions: “Update KYC” | “Security Checkup” | “Manage Devices”
–	Color: Gray.
–	CTA: “Open Settings”
Section 56.3 — Business Account Dashboards
•	Visual: 4 rich cards in 2x2 grid.
•	Card 1 — Payments & Collections Dashboard
–	Icon: Cash register with arrows.
–	Title: “Payments & Collections”
–	Description: “Collect from customers, pay suppliers, and manage your cash flow.”
–	Preview Metrics: “NGN 5.2M collected today | 12 pending payouts | 3 failed transactions”
–	Key Features List:
•	Payment links and checkout generation.
•	Invoice creation and tracking.
•	Bulk payout management.
•	Payment reconciliation (auto-match to invoices).
•	Refund and chargeback handling.
•	Multi-channel collection (mobile money, bank, card, QR).
–	Quick Actions: “Create Payment Link” | “Send Invoice” | “Process Payout”
–	Color: Navy.
–	CTA: “Open Payments”
•	Card 2 — Team & Payroll Dashboard
–	Icon: People with money.
–	Title: “Team & Payroll”
–	Description: “Manage employees, process payroll, and control team spending.”
–	Preview Metrics: “24 team members | Payroll due in 3 days | NGN 2.1M monthly payroll”
–	Key Features List:
•	Employee directory and onboarding.
•	Payroll processing (salary, bonuses, deductions).
•	Team expense cards with limits.
•	Approval workflows (expense, purchase, leave).
•	Attendance and time tracking integration.
•	Tax and pension compliance.
–	Quick Actions: “Process Payroll” | “Add Team Member” | “Review Expenses”
–	Color: Indigo.
–	CTA: “Open Team”
•	Card 3 — Analytics & Reports Dashboard
–	Icon: Chart with trend line.
–	Title: “Analytics & Reports”
–	Description: “Deep insights into your business finances, customer behavior, and growth metrics.”
–	Preview Metrics: “23% revenue growth MoM | 1,240 active customers | NGN 45M monthly volume”
–	Key Features List:
•	Revenue and expense analytics.
•	Customer cohort analysis.
•	Payment method performance comparison.
•	Cash flow forecasting.
•	Custom report builder.
•	Scheduled report delivery (email, API, SFTP).
•	Export to Excel, PDF, PowerPoint.
–	Quick Actions: “View Revenue Report” | “Create Custom Report” | “Export Data”
–	Color: Emerald.
–	CTA: “Open Analytics”
•	Card 4 — Business Settings Dashboard
–	Icon: Building with gear.
–	Title: “Business Settings”
–	Description: “Configure your business profile, compliance, integrations, and security.”
–	Preview Metrics: “KYB verified | 3 API integrations active | 2 pending approvals”
–	Key Features List:
•	Business profile and branding.
•	Bank account and settlement settings.
•	API keys and webhook configuration.
•	Integration management (accounting, e-commerce, CRM).
•	Compliance documents and regulatory filings.
•	Role and permission management.
–	Quick Actions: “Update KYB” | “Manage Integrations” | “Configure API”
–	Color: Slate.
–	CTA: “Open Settings”
Section 56.4 — Developer Account Dashboards
•	Visual: 4 rich cards in 2x2 grid.
•	Card 1 — API Dashboard
–	Icon: Terminal/Code.
–	Title: “API Console”
–	Description: “Monitor API usage, manage keys, and configure webhooks.”
–	Preview Metrics: “12,400 API calls today | 99.97% success rate | 2 active environments”
–	Key Features List:
•	API key management (create, rotate, revoke).
•	Usage analytics by endpoint, method, and time.
•	Error rate monitoring and alerting.
•	Webhook configuration and logs.
•	Rate limit status and quota usage.
•	API version management.
–	Quick Actions: “Generate New Key” | “View Logs” | “Test Endpoint”
–	Color: Violet.
–	CTA: “Open API Console”
•	Card 2 — Sandbox Environment
–	Icon: Flask/Test tube.
–	Title: “Sandbox”
–	Description: “Test integrations safely with simulated transactions and pre-loaded data.”
–	Preview Metrics: “340 test transactions | 8 test scenarios | Sandbox uptime: 100%”
–	Key Features List:
•	Pre-configured test scenarios (success, failure, pending, dispute).
•	Test customer and transaction data.
•	Webhook testing endpoint.
•	Sandbox-to-production migration guide.
•	Shared team sandbox (collaborative testing).
–	Quick Actions: “Run Test Scenario” | “View Sandbox Data” | “Reset Sandbox”
–	Color: Amber.
–	CTA: “Open Sandbox”
•	Card 3 — Documentation & Tools
–	Icon: Book/Wrench.
–	Title: “Docs & Tools”
–	Description: “Access comprehensive documentation, SDKs, and developer tools.”
–	Preview Metrics: “25 guides | 9 SDKs | 50+ code recipes”
–	Key Features List:
•	Interactive API explorer (try-it-now).
•	SDK downloads and installation guides.
•	Code recipes for common flows.
•	Changelog and deprecation notices.
•	Community forum and Discord access.
•	Support ticket creation.
–	Quick Actions: “Browse Docs” | “Download SDK” | “Join Community”
–	Color: Sky.
–	CTA: “Open Documentation”
•	Card 4 — App Management
–	Icon: App grid.
–	Title: “My Apps”
–	Description: “Manage your applications, review status, and monitor performance.”
–	Preview Metrics: “3 live apps | 1 in review | 12,000 monthly active users”
–	Key Features List:
•	App registration and configuration.
•	Production access request workflow.
•	App performance metrics (latency, error rates).
•	User feedback and crash reports.
•	Marketplace listing management (if applicable).
–	Quick Actions: “Register New App” | “Request Production Access” | “View Analytics”
–	Color: Rose.
–	CTA: “Open App Management”
Section 56.5 — Loans & Credit Dashboard (Cross-Cutting)
•	Visual: Special featured card spanning full width (if user has credit products or is eligible).
•	Icon: Money with growth arrow.
•	Title: “Loans & Credit”
•	Description: “Access working capital, manage existing loans, and explore financing options.”
•	Preview Metrics: “Credit limit: NGN 2M | Outstanding: NGN 500K | Next payment: 5 days”
•	Key Features List:
–	Loan application and status tracking.
–	Credit limit management.
–	Repayment schedule and history.
–	Early repayment options.
–	Credit score monitoring (where available).
–	BNPL transaction management.
–	Refinancing options.
•	Quick Actions: “Apply for Loan” | “Make Payment” | “View Credit Score”
•	Color: Gold/Amber gradient.
•	Eligibility Badge: “Pre-approved for NGN 2M” or “Check your eligibility”
•	CTA: “Open Loans & Credit”
Section 56.6 — Custom Dashboard Creation (Enterprise)
•	Visual: “Create Custom Dashboard” card for enterprise users.
•	Content: “Build a dashboard tailored to your specific KPIs and workflows.”
•	Features: Drag-and-drop widgets, custom data sources, scheduled exports, team sharing.
•	CTA: “Create Custom Dashboard”
Section 56.7 — Recent Notifications & Alerts
•	Visual: Sidebar or bottom strip.
•	Content: Unread notifications per dashboard (e.g., “Transactions: 3 new alerts” | “Bills: 2 due soon”).
•	Dismissible: Users can clear or mark as read.
Section 56.8 — Quick Search & Command Palette
•	Visual: Floating search bar or Cmd+K shortcut.
•	Content: “Search dashboards, transactions, settings, or get help…”
•	Results: Instant navigation to any dashboard, transaction, or help article.
Section 56.9 — CTA: “Go to [Selected Dashboard]”
•	Visual: Large primary button that updates based on selected card.
•	Behavior: Clicking a dashboard card opens it; clicking CTA confirms selection and navigates.
________________________________________
 ## PAGE 57: SESSION MANAGEMENT & SECURITY CENTER URL: /security
Goal: Empower users to monitor and control their account security.
Audience: Security-conscious users, enterprise admins, users who suspect unauthorized access.
Section 57.1 — Security Overview Dashboard
•	Visual: Security score circle (0–100) with color coding.
•	Headline: “Security Center”
•	Subheadline: “Monitor your account security and manage active sessions.”
•	Security Score: “Your security score: 85/100” with improvement suggestions.
•	Score Components:
–	Strong password: +20
–	2FA enabled: +25
–	Passkey enrolled: +20
–	Biometric enabled: +10
–	Recent security review: +10
–	No suspicious activity: +15
Section 57.2 — Active Sessions
•	Visual: Session list with device icons and maps.
•	Columns: Device, Location, IP Address, Last Active, Status.
•	Example Entries:
–	“iPhone 15 Pro — Lagos, Nigeria — 192.168.x.x — Active now — This device”
–	“Chrome on MacBook — Nairobi, Kenya — 197.x.x.x — 2 hours ago — Active”
–	“Safari on iPad — Accra, Ghana — 154.x.x.x — 3 days ago — Inactive”
•	Actions per Session:
–	“Log out this device” (individual revocation).
–	“Log out all other devices” (mass revocation).
–	“Mark as trusted” / “Mark as untrusted.”
•	Auto-Logout Settings: “Log me out after [15 min / 1 hour / 8 hours / Never] of inactivity.”
Section 57.3 — Login History
•	Visual: Filterable table with 90-day history.
•	Columns: Date/Time, Device, Browser, Location, IP, Method, Status.
•	Status: Success / Failed / Blocked / Step-up Required.
•	Filter: By date range, by status, by device, by location.
•	Export: Download as CSV/PDF.
•	Anomaly Highlighting: Unusual entries flagged with “⚠️ Unusual location” or “⚠️ New device.”
Section 57.4 — Trusted Devices
•	Visual: Device management grid.
•	Content: Devices explicitly marked as trusted (skip 2FA, longer session duration).
•	Management: Add/remove trusted devices, rename devices, view device details.
•	Limit: Max 10 trusted devices (prevents abuse).
Section 57.5 — Security Alerts & Notifications
•	Visual: Alert history with severity indicators.
•	Alert Types:
–	New device login.
–	Password changed.
–	2FA method added/removed.
–	Large transaction initiated.
–	Failed login attempts.
–	API key created/rotated.
–	Suspicious activity detected.
•	Delivery Preferences: Email, SMS, push notification, in-app.
•	Alert Settings: Customize thresholds and delivery methods per alert type.
Section 57.6 — Security Recommendations
•	Visual: Actionable checklist with progress.
•	Recommendations:
–	☐ Enable 2FA (if not enabled).
–	☐ Set up a passkey (if not enrolled).
–	☐ Review and update security questions.
–	☐ Generate new recovery codes.
–	☐ Review connected third-party apps.
–	☐ Update password (if older than 6 months).
–	☐ Enable login notifications.
•	One-Click Actions: Each recommendation has a direct link to complete it.
Section 57.7 — Account Lock & Emergency Freeze
•	Visual: Prominent but safe emergency controls.
•	Temporary Lock: “Lock my account for 24 hours” (prevents all logins and transactions, reversible with identity verification).
•	Emergency Freeze: “Freeze all cards and transactions immediately” (for suspected fraud, requires phone call to unfreeze).
•	Panic Button: “I suspect unauthorized access — secure my account now” (triggers all protective measures at once).
Section 57.8 — Third-Party App Access
•	Visual: Connected apps list with permissions.
•	Content: OAuth-connected apps with granted permissions (read transactions, initiate payments, etc.).
•	Management: Revoke access, review permissions, see last used date.
•	Risk Score: Each app rated for permission breadth and trustworthiness.
________________________________________
 ## PAGE 58: BIOMETRIC SETUP & PASSKEY MANAGEMENT URL: /security/biometrics
Goal: Guide users through passwordless authentication setup.
Audience: Users wanting enhanced security and convenience.
Section 58.1 — Passkey & Biometric Overview
•	Visual: Comparison table: Password vs. Passkey vs. Biometric.
•	Headline: “Go Passwordless — It’s Faster and More Secure.”
•	Subheadline: “Set up passkeys and biometrics for instant, phishing-resistant login.”
•	Benefits:
–	🔒 Phishing-resistant (can’t be stolen via fake websites).
–	⚡ Faster login (no typing, just touch or glance).
–	🌍 Works across devices (synced via platform authenticators).
–	🛡️ No password to forget or leak.
Section 58.2 — Passkey Setup Wizard
•	Visual: Step-by-step wizard with platform-specific instructions.
•	Step 1 — Check Compatibility: Auto-detect if device/browser supports WebAuthn/FIDO2.
•	Step 2 — Create Passkey:
–	Trigger browser/platform native prompt.
–	“Use your device’s security — Face ID, Touch ID, Windows Hello, or Android fingerprint.”
–	Backup options: “Save to this device” or “Save to password manager (1Password, Dashlane, iCloud Keychain).”
•	Step 3 — Name Your Passkey: “e.g., ‘iPhone 15’ or ‘Work Laptop’” (for management).
•	Step 4 — Test Passkey: Prompt user to authenticate with new passkey to confirm working.
•	Step 5 — Success: “Your passkey is ready! You can now sign in without a password.”
Section 58.3 — Biometric Enrollment (Mobile)
•	Visual: Mobile-optimized instructions with device mockups.
•	Face ID Setup (iOS):
–	Go to Settings → Face ID & Passcode.
–	Enable Face ID for Paymo app.
–	Test within app.
•	Fingerprint Setup (Android):
–	Go to Settings → Security → Fingerprint.
–	Register fingerprint.
–	Enable in Paymo app settings.
•	Fallback: PIN/Pattern always required as backup (biometric can fail).
Section 58.4 — Manage Passkeys
•	Visual: Passkey list with details.
•	Columns: Name, Device, Created Date, Last Used, Status.
•	Actions:
–	Rename passkey.
–	Remove passkey (with confirmation: “Are you sure? You’ll need to use password to sign in from this device.”).
–	Set as primary (default passkey for auto-prompt).
•	Sync Status: “Synced via iCloud Keychain” / “Synced via Google Password Manager” / “Device-only.”
Section 58.5 — Cross-Device Passkeys
•	Visual: QR code pairing animation.
•	Content: “Sign in on a new device using your phone’s passkey.”
•	Process:
–	On new device: Select “Sign in with passkey on another device.”
–	Scan QR code with phone.
–	Authenticate on phone (Face ID/Touch ID).
–	New device logged in, new passkey auto-registered.
Section 58.6 — Recovery Without Passkey
•	Visual: Recovery pathway diagram.
•	Content: “If you lose all your passkeys, you can still recover your account using:”
•	Methods: Email + password + 2FA, or security questions + identity verification, or support-assisted recovery.
•	Recommendation: “Always keep at least one traditional authentication method active as backup.”
Section 58.7 — Enterprise Passkey Management
•	Visual: Admin controls for enterprise.
•	Content: “Enterprise admins can mandate passkey usage for team members.”
•	Features:
–	Require passkey for all admin accounts.
–	Disable password-only login for sensitive roles.
–	Bulk passkey enrollment for corporate devices.
–	Passkey audit report (who has enrolled, who hasn’t).
________________________________________
 ## PAGE 59: ACCOUNT RECOVERY & IDENTITY VERIFICATION URL: /auth/identity-verification
Goal: High-assurance identity verification for account recovery and high-risk actions.
Audience: Users undergoing recovery, users triggering step-up verification.
Section 59.1 — Identity Verification Gateway
•	Visual: Serious but supportive tone (not alarming).
•	Headline: “Verify Your Identity”
•	Subheadline: “We need to confirm it’s really you. This protects your account from unauthorized access.”
•	Context Banner: “Reason for verification: [Account recovery / Large transaction / Sensitive action / Regulatory requirement]”
Section 59.2 — Verification Method Selection
•	Visual: Method cards based on user’s enrolled options and risk level.
•	Level 1 — Basic (Low Risk):
–	Email OTP + SMS OTP (dual-channel).
–	Security questions (2 of 3).
•	Level 2 — Standard (Medium Risk):
–	Government ID upload + selfie match.
–	Video selfie (liveness detection + agent review).
–	Bank account micro-deposit verification.
•	Level 3 — High Assurance (High Risk):
–	Video call with live agent (scheduled within 4 hours).
–	Document courier verification (for enterprise).
–	Notarized affidavit (for legal disputes).
Section 59.3 — Document Upload Verification
•	Visual: Guided upload interface.
•	Step 1 — Select Document Type: Passport, National ID, Driver’s License (country-specific options).
•	Step 2 — Capture/Upload:
–	Camera capture with real-time quality feedback (lighting, framing, glare).
–	Upload from device (JPEG, PNG, PDF supported).
–	Auto-crop and enhancement.
•	Step 3 — Selfie Match:
–	Live camera capture with liveness instructions (turn left, blink, smile).
–	Real-time face match against document photo.
–	Confidence score display (typically >95% for auto-approval).
•	Step 4 — Review:
–	“We’re reviewing your documents. This usually takes 2–5 minutes.”
–	Progress bar with estimated time.
–	Option to continue browsing (notification when complete).
Section 59.4 — Video Call Verification
•	Visual: Scheduling interface.
•	Content: “Schedule a 5-minute video call with our verification team.”
•	Availability: Calendar with available slots (next 48 hours).
•	Requirements: Valid ID present, good lighting, quiet environment, stable internet.
•	Process: Join video call → Show ID to camera → Answer security questions → Agent confirms → Account restored.
•	Languages: English, French, Portuguese, Swahili, Arabic, Hausa, Yoruba, Zulu.
Section 59.5 — Micro-Deposit Verification
•	Visual: Bank account input form.
•	Content: “We’ll send a small deposit (and withdrawal) to your linked bank account. Confirm the amounts to verify ownership.”
•	Process:
–	Enter bank account details (account number, bank name).
–	Paymo sends 2 micro-deposits (e.g., $0.23 and $0.47).
–	User checks bank statement and enters amounts in Paymo.
–	Match confirms account ownership.
•	Timeline: Deposits arrive in 1–2 business days (instant for supported banks via API).
Section 59.6 — Verification Status Tracking
•	Visual: Progress tracker.
•	Steps: Submitted → Under Review → Additional Info Required / Approved / Rejected.
•	Notifications: Email and push updates at each stage.
•	Escalation: If rejected, clear reason given with re-submission instructions.
Section 59.7 — Post-Verification Actions
•	Visual: Success confirmation with next steps.
•	Account Recovery: “Your account has been restored. Please set a new password and review your security settings.”
•	High-Risk Action: “Identity verified. You may now proceed with [action].”
•	Regulatory: “KYC updated. Your account limits have been increased.”
________________________________________
 ## PAGE 60: LOGIN ACTIVITY & FRAUD ALERTS URL: /security/alerts
Goal: Real-time security monitoring and user empowerment against fraud.
Audience: All users, especially those in high-risk contexts.
Section 60.1 — Fraud Alert Dashboard
•	Visual: Alert inbox with severity indicators.
•	Headline: “Security Alerts”
•	Subheadline: “Stay informed about activity on your account.”
•	Unread Counter: “3 unread alerts” badge.
•	Alert Categories:
–	🔴 Critical: Unauthorized access attempt, large unauthorized transaction, account lock.
–	🟠 Warning: New device login, password changed, 2FA modified, unusual location.
–	🟡 Info: Successful login from new device, API key rotation, scheduled maintenance.
–	🔵 Success: Security improvement completed, verification successful.
Section 60.2 — Real-Time Alert Feed
•	Visual: Chronological feed with rich details.
•	Alert Card Example:
–	“🔴 Critical — June 11, 2026, 03:14 AM”
–	“Login attempt blocked from Moscow, Russia (IP: 185.x.x.x)”
–	“Device: Unknown Chrome on Windows”
–	“Action taken: Blocked after 3 failed attempts. Account temporarily locked.”
–	“Your action: [Unlock Account] [Confirm this was me] [Contact Support]”
•	Rich Context: Map showing location, device fingerprint, time zone difference.
Section 60.3 — Alert Response Actions
•	Visual: Action buttons per alert.
•	“This was me” — Mark as legitimate, add device/location to trusted list.
•	“This wasn’t me” — Trigger account lock, force password reset, revoke all sessions, initiate fraud investigation.
•	“I’m not sure” — Temporary lock + support contact.
•	“Dismiss” — Acknowledge and archive (not available for critical alerts).
Section 60.4 — Fraud Prevention Tips
•	Visual: Educational cards.
•	“Never share your PIN or password with anyone — Paymo will never ask for it.”
•	“Check the URL before entering credentials: always paymo.co (not paymo-secure.com or similar).”
•	“Enable push notifications for all login attempts.”
•	“Use a unique password for Paymo — don’t reuse from other sites.”
•	“Be wary of urgent messages asking you to ‘verify your account immediately.’”
Section 60.5 — Report Fraud
•	Visual: Report form.
•	Content: “Suspect fraudulent activity? Report it immediately.”
•	Form Fields:
–	Type of fraud (unauthorized transaction, phishing, identity theft, card fraud, other).
–	Description of incident.
–	Date/time of incident.
–	Amount involved (if applicable).
–	Supporting documents (screenshots, emails, receipts).
•	Response: Auto-acknowledgment, investigation within 24 hours, dedicated fraud specialist assigned.
•	Emergency Hotline: 24/7 fraud hotline number.
Section 60.6 — Fraud Protection Settings
•	Visual: Toggle settings.
•	Login Notifications: Notify on every login (on/off).
•	Transaction Alerts: Notify on transactions > [customizable threshold].
•	Location Alerts: Notify when login is from >100km from usual location.
•	Device Alerts: Notify on every new device.
•	API Activity Alerts: Notify on API key creation or high-volume usage.
•	Quiet Hours: Pause non-critical alerts during specified hours.
Section 60.7 — Fraud Resolution Timeline
•	Visual: Timeline infographic.
•	Report Received: Auto-acknowledgment within 5 minutes.
•	Initial Review: Fraud analyst assigned within 2 hours.
•	Investigation: Evidence gathering, transaction tracing, partner coordination (24–72 hours).
•	Resolution: Funds recovery (if possible), account restoration, security recommendations.
•	Follow-up: Post-resolution check-in, security review offer.
Section 60.8 — CTA: “Stay Protected”
•	CTAs: “Review Security Settings” | “Enable All Alerts” | “Contact Fraud Team”
________________________________________
AUTHENTICATION FLOW DIAGRAMS
Flow 1: Standard Login (Returning User with Passkey)
User visits /auth/login
→ Auto-detects passkey enrollment
→ Triggers WebAuthn prompt (Face ID/Touch ID/Windows Hello)
→ Biometric verified
→ Risk check (device known, location normal)
→ Redirect to /auth/account-type
→ User selects account type
→ Redirect to /dashboard/select
→ User selects dashboard (e.g., Transactions)
→ Load Transactions Dashboard
Flow 2: Login with Password + 2FA
User visits /auth/login
→ Selects Password tab
→ Enters email + password
→ Password validated
→ Check: Is 2FA enabled? YES
→ Redirect to /auth/mfa
→ User selects TOTP/SMS/Push/Biometric
→ Factor verified
→ Risk check
→ Redirect to /auth/account-type
→ Continue as Flow 1
Flow 3: New User Registration
User visits /auth/register
→ Selects account type (Personal/Business/Developer)
→ Enters basic information
→ Completes KYC/KYB
→ Sets password + PIN
→ Prompted to set up passkey (optional)
→ Email verification sent
→ Account created
→ Redirect to /auth/account-type
→ User sees account type cards
→ Selects primary account
→ Redirect to /dashboard/select
→ Guided tour of selected dashboard
Flow 4: Account Recovery
User visits /auth/recovery
→ Selects recovery method (Email/SMS/Security Questions)
→ Completes verification
→ Sets new password/PIN
→ Mandatory security review (check recent activity, revoke sessions)
→ Redirect to /auth/login
→ Normal login flow
Flow 5: Risk-Based Step-Up
User logs in successfully
→ Risk engine flags: New country detected (traveling)
→ Intercept: Redirect to /auth/mfa
→ Additional factor required (not just password)
→ User completes step-up
→ Option: "Add this location to trusted list?"
→ Continue to dashboard
________________________________________
MASTER PAGE INDEX (Pages 1–60)
Page #	URL	Title	Category
51	/auth/login	Authentication Gateway	Auth
52	/auth/register	Create Account	Auth
53	/auth/recovery	Forgot Password/PIN	Auth
54	/auth/mfa	MFA Challenge	Auth
55	/auth/account-type	Account Type Selection	Auth
56	/dashboard/select	Dashboard Selection Hub	Auth
57	/security	Session Management & Security Center	Auth
58	/security/biometrics	Biometric Setup & Passkey Management	Auth
59	/auth/identity-verification	Account Recovery & Identity Verification	Auth
60	/security/alerts	Login Activity & Fraud Alerts	Auth
Total Architecture: 60 Pages | ~230,000+ characters | ~46,000+ words
________________________________________
End of Authentication Architecture Document



 # PayMo BaaS Fintech — Dashboard 4: End-User Lending & Credit Portal

**Purpose:** The borrower-facing interface where retail consumers, SME owners, corporate treasurers, and real estate developers interact with PayMo's lending products. This is the customer self-service layer built on top of Dashboard 3's admin infrastructure.

**Users:** Individual borrowers, business owners, finance managers, property developers — anyone who borrows from PayMo.

---

## Page 4.1 — Borrower Home / Credit Dashboard

**Purpose:** Central hub showing the borrower's complete credit relationship with PayMo.

### Sections & Content:

1. **Credit Health Scorecard**
   - PayMo Credit Score (internal, 300-850 scale)
   - Score trend (last 6 months)
   - Factors affecting score: payment history, credit utilization, account age, recent inquiries
   - Tips to improve score
   - Comparison to average score in segment

2. **Active Credit Summary**
   - Total outstanding balance across all facilities
   - Total credit limit (for revolving products)
   - Available credit (unused portion)
   - Next payment due: amount, date, countdown
   - Days until next due date
   - Auto-debit status (active/inactive)

3. **Quick Action Bar**
   - Make a payment
   - Apply for new loan / top-up
   - Download statement
   - Chat with support
   - Request payment holiday
   - Update bank details

4. **Payment Calendar**
   - Visual calendar view of all upcoming payments
   - Color-coded: paid (green), upcoming (blue), overdue (red)
   - Tap to see payment details
   - Add to personal calendar (Google/Apple/Outlook)

5. **Recent Activity Feed**
   - Last 5 transactions: payments, disbursements, fee charges, interest postings
   - Timestamp and amount
   - Tap for full details

6. **Promotions & Offers**
   - Pre-approved loan offers
   - Loyalty rewards (reduced rate for good payers)
   - Referral program banner
   - Product recommendations based on profile

---

## Page 4.2 — Apply for a Loan

**Purpose:** Streamlined loan application flow for all PayMo products.

### Sections & Content:

1. **Product Selector**
   - Visual cards for available products:
     - **Personal:** Quick Cash, Salary Advance, Education, Medical, Travel, Asset Finance
     - **Business:** Working Capital, Invoice Finance, Equipment, Trade Finance, Merchant Advance
     - **Real Estate:** Home Loan, Construction, Land Purchase, Refinance
   - Product details on tap: amount range, tenor, rate, requirements
   - "Not sure?" → Product recommendation wizard

2. **Loan Calculator**
   - Slider for desired amount
   - Slider for desired tenor
   - Real-time calculation:
     - Monthly/weekly repayment
     - Total interest payable
     - Total repayment amount
     - APR display
   - Compare different tenors side-by-side
   - Affordability indicator (green/yellow/red based on DTI)

3. **Application Form**
   - **Step 1 — Purpose:** Select loan purpose from dropdown
   - **Step 2 — Amount & Tenor:** Confirm or adjust from calculator
   - **Step 3 — Personal/Business Details:** Auto-populated from profile, editable
   - **Step 4 — Income/Financials:**
     - Retail: Employment status, employer, monthly income, other income
     - SME: Business revenue, bank statements upload, tax returns
     - Corporate: Financial statements, board resolution
     - Real Estate: Property details, construction cost estimate, income projections
   - **Step 5 — Documents:** Camera upload for ID, proof of address, bank statements, payslips, property documents
   - **Step 6 — Review & Submit:** Full application summary, terms acceptance, digital signature

4. **Application Status Tracker**
   - Post-submission tracking widget
   - Stages: Submitted → Under Review → Additional Info Needed → Approved → Disbursed
   - Current stage highlight with estimated time
   - Push notifications at each stage change
   - "Why is this taking long?" → Explanation and contact option

5. **Counter-Offer Handling**
   - If approved for less than requested: Accept/decline counter-offer
   - If declined: Reason explanation, improvement suggestions, reapply timeline
   - If conditional: List of conditions to fulfill

---

## Page 4.3 — My Loans / Credit Facilities

**Purpose:** Complete view and management of all active and closed credit facilities.

### Sections & Content:

1. **Active Facilities List**
   - Card view per facility:
     - Product name and icon
     - Original amount vs. outstanding
     - Progress bar (percentage repaid)
     - Next due date and amount
     - Status: Current, Grace Period, Overdue
   - Sort: by due date, by balance, by product

2. **Facility Detail View**
   - **Summary Tab:**
     - Disbursement date and amount
     - Current principal outstanding
     - Accrued interest
     - Total balance
     - Interest rate and type
     - Remaining tenor
   - **Repayment Schedule Tab:**
     - Full amortization table
     - Paid installments (strikethrough/green)
     - Upcoming installments
     - Total interest over life of loan
   - **Transactions Tab:**
     - All disbursements, repayments, fees, interest postings
     - Filter by type and date range
     - Download transaction history
   - **Documents Tab:**
     - Loan agreement
     - Terms and conditions
     - Insurance documents
     - Valuation reports (real estate)
     - Statements

3. **Closed Facilities**
   - Historical loans with closure date
   - Total repaid amount
   - Closure certificate download
   - "Reapply" quick button

4. **Revolving Credit Management (Credit Line / Overdraft)**
   - Credit limit display
   - Used vs. available (visual gauge)
   - Current balance and interest accrued
   - Drawdown history
   - Minimum payment due
   - Credit limit increase request

---

## Page 4.4 — Make a Payment

**Purpose:** Flexible repayment interface with multiple options.

### Sections & Content:

1. **Payment Overview**
   - Total amount due (principal + interest + fees)
   - Minimum due vs. full balance (for revolving)
   - Overdue amount (if any) with penalty breakdown
   - Days overdue indicator

2. **Payment Amount Selection**
   - Preset buttons: Minimum Due, Full Balance, Custom Amount
   - Custom amount input with validation
   - Partial payment acknowledgment
   - "Pay extra to reduce principal" option

3. **Payment Method Selection**
   - **PayMo Wallet:** Instant deduction (if sufficient balance)
   - **Linked Bank Account:** Select saved account or add new
   - **Mobile Money:** M-Pesa, Airtel Money, etc. (STK push)
   - **Debit/Credit Card:** Saved cards or add new (tokenized)
   - **Cash:** Agent locator map for cash deposit
   - **Salary Deduction:** Toggle auto-deduct from payroll (if employer partnered)

4. **Payment Scheduling**
   - Pay now
   - Schedule for future date
   - Set up recurring auto-payment (weekly, monthly, on due date)

5. **Payment Confirmation**
   - Final amount and method review
   - Digital receipt generation
   - Payment reference number
   - Share receipt (WhatsApp, email, PDF)
   - Update repayment schedule preview

6. **Payment History**
   - All past payments with date, amount, method
   - Filter by facility and date range
   - Download payment certificate
   - Dispute a payment option

---

## Page 4.5 — Top-Up & Additional Credit

**Purpose:** Existing borrowers requesting additional funds or new products.

### Sections & Content:

1. **Eligibility Checker**
   - Pre-qualified amount based on payment history and current balance
   - "You're eligible for up to $X" banner
   - Reasons if not eligible with improvement path

2. **Top-Up Request**
   - Select facility to top-up
   - Requested amount (within eligible limit)
   - Purpose of top-up
   - New repayment terms (if extended)
   - Instant approval for small amounts with good history
   - Larger amounts → underwriting review

3. **Parallel Loan Application**
   - Apply for different product while existing loan active
   - Combined DTI check
   - Cross-collateralization options

4. **Credit Limit Increase (Revolving)**
   - Requested new limit
   - Income update if changed
   - Automatic vs. manual review threshold

5. **Consolidation Offer**
   - "Consolidate your loans" calculator
   - Single new loan to pay off multiple existing
   - New rate vs. blended old rate
   - Simplified single payment

---

## Page 4.6 — Statements & Documents

**Purpose:** Self-service access to all loan-related documentation.

### Sections & Content:

1. **Statement Generator**
   - Select facility and date range
   - Statement types: repayment, interest, full account
   - Generate and download PDF
   - Email statement to self or accountant

2. **Tax Documents**
   - Annual interest paid certificate (for tax deduction)
   - Withholding tax certificates
   - Year-end summary

3. **Loan Documents Vault**
   - Original loan agreement
   - Amendments and variations
   - Security documents (mortgage deed, guarantee)
   - Insurance policies
   - Valuation reports
   - All with download and share options

4. **No-Objection Certificates**
   - Request NOC for partial collateral release
   - Request NOC for loan closure
   - Track request status

---

## Page 4.7 — Collateral & Security (Borrower View)

**Purpose:** Transparency on assets pledged to PayMo.

### Sections & Content:

1. **My Collateral Summary**
   - List of all pledged assets
   - Type, description, current status
   - Linked loan facility

2. **Real Estate Collateral**
   - Property address and details
   - Current valuation and date
   - LTV ratio
   - Insurance status and expiry
   - Inspection schedule notifications

3. **Movable Assets**
   - Vehicle: make, model, registration, tracking status
   - Equipment: description, location
   - Securities: holdings, market value

4. **Cash Collateral**
   - Fixed deposit details
   - Interest earned
   - Release conditions

5. **Collateral Release Request**
   - Request partial or full release
   - Reason selection
   - Substitution offer (if applicable)
   - Track request status

---

## Page 4.8 — Restructuring & Hardship

**Purpose:** Self-service options for borrowers facing repayment difficulties.

### Sections & Content:

1. **Financial Hardship Declaration**
   - Reason selection: job loss, medical emergency, business downturn, natural disaster, other
   - Supporting document upload
   - Current financial situation disclosure
   - Privacy-assured process

2. **Relief Options Explorer**
   - Payment holiday (1-3 months)
   - Reduced installment amount
   - Extended tenor
   - Interest-only period
   - Temporary rate reduction
   - Impact calculator for each option

3. **Restructuring Application**
   - Preferred option selection
   - New proposed terms
   - Supporting rationale
   - Digital signature
   - Review timeline: 3-5 business days

4. **Forbearance Status**
   - Current forbearance details (if active)
   - Remaining forbearance period
   - Exit plan and resumption date
   - New repayment schedule post-forbearance

5. **Credit Impact Transparency**
   - Clear explanation of restructuring impact on credit score
   - Difference between "restructured" and "default" reporting
   - Path back to normal status

---

## Page 4.9 — Credit Score & Financial Wellness

**Purpose:** Financial education and credit health improvement tools.

### Sections & Content:

1. **PayMo Credit Score**
   - Current score with visual gauge
   - Score history graph (6/12/24 months)
   - Score factors breakdown:
     - Payment history (35%)
     - Credit utilization (30%)
     - Length of credit history (15%)
     - Credit mix (10%)
     - New inquiries (10%)

2. **Credit Report**
   - Full credit report download
   - Accounts listed with status
   - Inquiry history
   - Dispute incorrect information

3. **Financial Wellness Tools**
   - Debt-to-income calculator
   - Affordability calculator
   - Budget planner
   - Savings goal tracker
   - Emergency fund calculator

4. **Credit Education**
   - Articles: "How to improve your credit score"
   - Videos: Understanding interest rates
   - Tips: Avoiding predatory lending
   - Quiz: Financial literacy assessment

5. **Goal Setting**
   - "I want to improve my score by X points in Y months"
   - Action plan with milestones
   - Progress tracking

---

## Page 4.10 — Settings & Account Management

**Purpose:** Borrower profile and preference management.

### Sections & Content:

1. **Personal/Business Profile**
   - View and edit contact details
   - Employment/business information update
   - Income update (triggers re-evaluation)

2. **Bank Accounts & Cards**
   - Linked accounts for auto-debit
   - Add/remove bank accounts (micro-deposit verification)
   - Saved debit/credit cards
   - Default payment method selection

3. **Notification Preferences**
   - Payment reminders: SMS, email, push, WhatsApp
   - Due date: 3 days before, 1 day before, on day
   - Marketing communications toggle
   - Statement delivery: email, app only, postal

4. **Security Settings**
   - Change password/PIN
   - Biometric login setup
   - Two-factor authentication
   - Login history and device management
   - Suspend account temporarily

5. **Privacy & Data**
   - Data sharing consent management
   - Download my data (GDPR/CCPA style)
   - Account deletion request
   - Marketing opt-out

---

## Page 4.11 — Support & Disputes

**Purpose:** Customer service interface for loan-related issues.

### Sections & Content:

1. **Help Center**
   - Searchable FAQ
   - Topics: payments, statements, applications, collateral, hardship
   - Video tutorials
   - Chatbot for instant answers

2. **Live Chat / Callback Request**
   - Chat with human agent
   - Schedule callback at preferred time
   - Priority queue for overdue accounts

3. **Raise a Dispute**
   - Dispute types: incorrect charge, payment not reflected, statement error, insurance issue
   - Description and evidence upload
   - Dispute reference and tracking
   - SLA: resolution within 10 business days

4. **Complaint Escalation**
   - Internal complaint register
   - Escalation to regulator option (if unresolved)
   - Complaint status tracking
   - Final response documentation

5. **Branch/Agent Locator**
   - Map view of nearby PayMo agents
   - Operating hours
   - Services available at each location
   - Directions integration

---

## Page 4.12 — Business Borrower Portal (SME/Corporate)

**Purpose:** Enhanced interface for business and corporate borrowers with additional features.

### Sections & Content:

1. **Business Credit Dashboard**
   - Total facilities: term loans, revolving credit, trade finance
   - Utilization vs. limits
   - Available headroom
   - Next board reporting date

2. **Multi-User Access**
   - Admin user management
   - Role assignment: view only, initiate payment, approve, admin
   - Approval limits per user
   - Activity log per user

3. **Drawdown Request (Revolving Facilities)**
   - Available facility selection
   - Drawdown amount
   - Purpose certification
   - Supporting document upload
   - Approval workflow (if internal approval required)

4. **Covenant Self-Reporting**
   - Upload quarterly/semi-annual financials
   - Auto-populated covenant calculation preview
   - Compliance certificate submission
   - Upcoming reporting deadlines

5. **Trade Finance Module**
   - Letter of Credit application
   - Guarantee request
   - Invoice financing upload
   - Shipping document tracking
   - Status updates from PayMo trade desk

6. **Treasury Integration**
   - Link to corporate treasury system (API)
   - Cash position view
   - Automated repayment from designated accounts

---

## Page 4.13 — Real Estate Borrower Portal

**Purpose:** Specialized interface for property developers and homeowners.

### Sections & Content:

1. **Project Dashboard (Construction Finance)**
   - Project name and location
   - Total approved facility
   - Disbursed to date
   - Remaining available
   - Construction progress tracker

2. **Milestone Management**
   - Milestone schedule with completion criteria
   - Upload completion certificates
   - Architect/engineer sign-off request
   - Inspection report status
   - Next disbursement trigger status

3. **Property Details (Mortgage)**
   - Property address and description
   - Current valuation
   - Outstanding mortgage balance
   - Equity (property value - loan balance)
   - LTV ratio trend

4. **Insurance Management**
   - Required insurance types
   - Current policies and expiry dates
   - Upload renewal certificates
   - Premium payment tracking

5. **Refinancing & Top-Up**
   - Current rate vs. market rate comparison
   - Refinancing savings calculator
   - Equity release top-up eligibility
   - Application initiation

---

## Cross-Portal Features (All User Types)

| Feature | Description |
|---------|-------------|
| **Biometric Login** | Fingerprint, Face ID, PIN |
| **Push Notifications** | Due reminders, approval updates, disbursement alerts |
| **Offline Mode** | View balances and schedule payments offline (sync when connected) |
| **Multi-Language** | English, Swahili, French, Arabic, local languages |
| **Accessibility** | Screen reader support, high contrast, font sizing |
| **Dark/Light Mode** | Theme toggle matching Dashboard 1-3 admin portal |
| **Quick Actions Widget** | Home screen widget for instant payment/view balance |

---

## Integration with Admin Dashboard 3

| User Action | Portal 4 Flow | Dashboard 3 Trigger |
|-------------|---------------|---------------------|
| Submit loan application | Form → Upload → Submit | New application in pipeline, pre-screening auto-runs |
| Make payment | Select amount → Pay → Confirm | Real-time loan account posting, balance update |
| Request top-up | Eligibility check → Request → Submit | Top-up request queue, auto-approve or underwrite |
| Report hardship | Form → Documents → Submit | Restructuring workflow initiated, case assigned |
| Upload financials (corporate) | Upload → Auto-parse preview → Submit | Covenant testing auto-triggered, compliance updated |
| Request collateral release | Form → Reason → Submit | Collateral team review queue |

---

This Dashboard 4 completes the **four-pillar PayMo architecture**:

| Dashboard | User | Purpose |
|-----------|------|---------|
| **1** | PayMo Operations | Bank-to-bank transfers & payments |
| **2** | PayMo Operations | Value-added services & utilities |
| **3** | PayMo Credit Team | Internal lending operations & risk management |
| **4** | Borrowers (Retail/SME/Corporate/Real Estate) | Self-service loan management & application |

The borrower portal is designed for **trust, transparency, and ease** — reducing support burden while increasing repayment rates through proactive engagement tools.

 # PayMo BaaS Fintech — Dashboard 3: PayMo Lending & Credit Services

** Architecture:** PayMo operates as the **lender of record** — originating, underwriting, disbursing, servicing, and collecting on loans and credit facilities directly to retail consumers, SMEs, corporates, and real estate developers. PayMo's balance sheet or funded warehouse lines are the source of capital. Dashboard 3 is the **internal credit operations center** for PayMo's lending business.

---

## Dashboard 3 Overview

**Purpose:** End-to-end lending operations for PayMo as a direct lender offering:
- **Retail Lending:** Personal loans, salary advances, buy-now-pay-later (BNPL), credit cards
- **SME & Business Lending:** Working capital, invoice financing, equipment loans, trade finance
- **Corporate Lending:** Term loans, revolving credit facilities, project finance
- **Real Estate Lending:** Construction finance, mortgage/home loans, commercial real estate (CRE)

**Capital Structure:** PayMo deploys its own capital, warehouse facilities, or securitization programs 

---

## Page 3.1 — Lending Command Center

**Purpose:** Real-time strategic and operational overview of PayMo's entire lending book.

### Sections & Content:

1. **Portfolio Snapshot**
   - Total gross loan book (outstanding principal)
   - Net loan book (after provisions)
   - Breakdown by product: Retail | SME | Corporate | Real Estate
   - Breakdown by currency
   - Month-over-month growth rate

2. **Live Origination & Collection Ticker**
   - New applications submitted (real-time)
   - Loans approved and disbursed today
   - Repayments received today
   - Defaults/recoveries today
   - Auto-refresh every 5 seconds

3. **Key Lending KPIs**
   - Disbursement volume (today / MTD / YTD)
   - Collection rate vs. target
   - Portfolio at Risk (PAR): PAR 30, PAR 60, PAR 90
   - Non-Performing Loan (NPL) ratio
   - Cost of Risk (provisions / average loans)
   - Net Interest Margin (NIM)
   - Return on Assets (ROA) for lending division

4. **Product Performance Grid**
   - Performance per product line:
     | Product | Book Size | Avg Ticket | PAR 30 | NPL | Yield |
   - Color-coded health indicators
   - Trend arrows (improving/deteriorating)

5. **Cash Flow & Liquidity for Lending**
   - Capital deployed vs. capital available
   - Warehouse facility utilization
   - Upcoming maturities (principal repayments due)
   - Securitization pipeline
   - Liquidity gap forecast (linked to Dashboard 1 nostro positions)

6. **Actionable Alerts Queue**
   - Loans approaching maturity (30/60/90 days)
   - PAR 30+ accounts requiring follow-up
   - Covenant breaches (corporate/real estate)
   - Insurance expiries on collateral
   - Valuation reviews due
   - Credit limit overruns

---

## Page 3.2 — Loan Products & Pricing Engine

**Purpose:** Configure, manage, and price all PayMo loan products.

### Sections & Content:

1. **Product Catalog**
   - **Retail Products:**
     - Personal Loan (unsecured)
     - Salary Advance / Payroll Loan
     - Buy Now Pay Later (BNPL) — merchant-integrated
     - Credit Card / Line of Credit
     - Education Loan
     - Medical Emergency Loan
     - Asset Finance (vehicle, electronics)
   - **SME Products:**
     - Working Capital Loan
     - Invoice Financing / Factoring
     - Purchase Order Financing
     - Equipment / Machinery Loan
     - Trade Finance (L/C, guarantees)
     - Merchant Cash Advance
   - **Corporate Products:**
     - Term Loan
     - Revolving Credit Facility
     - Overdraft Facility
     - Project Finance
     - Bridge Loan
     - Syndicated Loan (where PayMo is lead)
   - **Real Estate Products:**
     - Residential Mortgage / Home Loan
     - Construction Finance
     - Commercial Real Estate (CRE) Loan
     - Land Acquisition Loan
     - Refinancing / Top-up Loan

2. **Product Configuration**
   - Eligibility criteria per product
   - Min/max loan amounts
   - Tenor ranges
   - Interest rate structures: flat, reducing balance, fixed, floating
   - Fee structure: processing fee, commitment fee, late fee, prepayment penalty
   - Collateral requirements per tier
   - Insurance requirements
   - Grace period rules

3. **Pricing Engine**
   - Risk-based pricing matrix
   - Base rate + risk margin + liquidity margin + operational margin
   - Customer segment pricing (premium, standard, high-risk)
   - Promotional pricing campaigns
   - Competitive pricing benchmark
   - Minimum yield floor enforcement

4. **Product Performance Analytics**
   - Volume and value per product
   - Default rate per product
   - Profitability per product (revenue minus cost of funds, provisions, ops cost)
   - Customer acquisition cost per product
   - Cross-sell and upsell rates

---

## Page 3.3 — Application Intake & Pre-Screening

**Purpose:** Capture and initially evaluate all loan applications from consumers and businesses.

### Sections & Content:

1. **Application Channels**
   - **Retail:** Mobile app, web portal, USSD, agent network, merchant POS
   - **SME:** Business portal, relationship manager submission, API (embedded finance partners)
   - **Corporate:** Direct RM submission, treasury portal, API integration
   - **Real Estate:** Developer portal, broker submission, direct application

2. **Application Form Builder**
   - Dynamic forms per product type
   - Fields: personal/business details, loan amount, purpose, tenor, income/revenue
   - Document upload: ID, proof of address, bank statements, payslips, financials
   - Consent for credit bureau check and data processing
   - Digital signature capture

3. **Application Pipeline Board**
   - Stages: Submitted → Data Verification → Pre-screened → Underwriting → Approved → Declined → Cancelled
   - Volume and value at each stage
   - Conversion funnel analytics
   - SLA breach alerts per stage
   - Assigned officer display

4. **Automated Pre-Screening**
   - Eligibility rule engine check
   - Credit bureau score pull (real-time API)
   - Identity verification (KYC/KYB)
   - Fraud detection screening
   - Watchlist and sanctions screening
   - Existing exposure check (single borrower limit)
   - Pre-screen score and recommendation

5. **Application Scoring**
   - Application scorecard output
   - Risk grade assignment (A to F or 1 to 10)
   - Auto-approve threshold (low risk, small ticket)
   - Auto-decline threshold (high risk, policy breach)
   - Manual review queue (medium risk)

---

## Page 3.4 — Credit Underwriting & Decisioning

**Purpose:** Comprehensive risk assessment and credit decision-making for PayMo as lender.

### Sections & Content:

1. **Retail Underwriting**
   - **Income Verification:**
     - Bank statement analysis (auto-parse via open banking)
     - Payslip verification
     - Employment verification API
     - Alternative data: mobile money history, utility payments, rental history
   - **Debt Burden Analysis:**
     - Existing debt obligations (credit bureau + internal)
     - Debt-to-income (DTI) ratio calculation
     - Disposable income assessment
   - **Behavioral Scoring:**
     - Transaction pattern analysis
     - Account stability scoring
     - Social graph analysis (where permitted)
   - **Decision:** Approve / Decline / Refer with conditions / Counter-offer

2. **SME Underwriting**
   - **Business Financial Analysis:**
     - 2-3 year financial statement review
     - Bank statement analysis (6-12 months)
     - Cash flow cycle analysis
     - Revenue trend and seasonality
   - **Business Credit Assessment:**
     - Business credit score
     - Trade reference checks
     - Supplier/customer concentration
   - **Owner/Director Assessment:**
     - Personal credit check
     - Personal guarantee evaluation
     - Background and experience review
   - **Decision:** Approve / Decline / Conditional / Counter-offer

3. **Corporate Underwriting**
   - **Financial Statement Analysis:**
     - Audited financials (3 years)
     - Ratio analysis: DSCR, ICR, leverage, liquidity
     - Cash flow modeling and projections
     - Peer benchmarking
   - **Business Risk Assessment:**
     - Industry analysis and outlook
     - Competitive position
     - Management quality assessment
     - ESG risk evaluation
   - **Facility Structuring:**
     - Amount, tenor, repayment structure
     - Security/collateral requirements
     - Covenant package design
     - Pricing negotiation
   - **Decision:** Credit committee approval required

4. **Real Estate Underwriting**
   - **Project/Property Assessment:**
     - Property valuation (independent appraiser)
     - Location and market analysis
     - Developer track record (construction finance)
     - Building plans and permits verification
     - Environmental assessment
   - **Financial Viability:**
     - Project cost breakdown and feasibility
     - Sales/rental projections (market comparables)
     - Loan-to-value (LTV) calculation
     - Debt service coverage ratio (DSCR)
     - Pre-sales/commitment level (construction)
   - **Legal & Title:**
     - Title deed verification
     - Encumbrance search
     - Construction contract review
     - Insurance requirements
   - **Decision:** Real estate credit committee approval

5. **Credit Memo & Committee Workflow**
   - Auto-generated credit memorandum
   - Risk rating and recommendation
   - Digital approval workflow
   - Approval authority matrix (by amount, product, risk grade)
   - Minutes and decision record
   - Appeal process for declined applications

---

## Page 3.5 — Loan Documentation & Agreement Management

**Purpose:** Legal documentation generation, execution, and storage for PayMo loans.

### Sections & Content:

1. **Document Generation Engine**
   - **Retail:** Loan agreement, terms and conditions, direct debit mandate, disclosure statements
   - **SME:** Loan agreement, security documents, personal guarantee, board resolution
   - **Corporate:** Facility agreement, security trust deed, intercreditor agreement (if syndicated), legal opinion
   - **Real Estate:** Mortgage deed, charge over property, construction contract, insurance certificates, valuation report

2. **Dynamic Clause Library**
   - Standard clauses per product and jurisdiction
   - Variable insertion: borrower name, amount, rate, tenor, collateral description
   - Special conditions based on risk grade
   - Regulatory required disclosures
   - Version control and legal approval workflow

3. **E-Signature & Execution**
   - Digital signature workflow (DocuSign/Adobe Sign/HelloSign)
   - SMS OTP for retail customers
   - Witness and notarization requirements (where applicable)
   - Execution certificate generation
   - Document delivery to borrower

4. **Conditions Precedent (CP) Management**
   - CP checklist per product type
   - Status tracking: pending, received, verified, waived
   - Document upload and verification
   - CP satisfaction certificate
   - Loan activation trigger

5. **Document Repository**
   - Centralized storage with folder structure per borrower
   - Document expiration tracking (ID, insurance, valuation)
   - Renewal reminders
   - Audit trail of document access
   - Regulatory retention compliance

---

## Page 3.6 — Disbursement Management

**Purpose:** Controlled release of PayMo loan funds to approved borrowers.

### Sections & Content:

1. **Disbursement Queue**
   - Approved loans awaiting disbursement
   - CP completion status
   - Disbursement amount and account details
   - Priority ordering (urgent, standard)

2. **Disbursement Execution**
   - **Retail:** Direct to borrower's PayMo wallet or linked bank account
   - **SME:** To business operating account or supplier account (trade finance)
   - **Corporate:** To designated disbursement account per facility agreement
   - **Real Estate:** Staged disbursement to escrow or developer account tied to construction milestones
   - Payment rail selection (linked to Dashboard 1)
   - Disbursement confirmation and receipt

3. **Staged/Milestone Disbursement (Real Estate & Project Finance)**
   - Milestone definition and approval
   - Architect/engineer certification upload
   - Inspection report verification
   - Stage completion trigger
   - Partial disbursement execution
   - Cumulative disbursement tracking vs. total facility

4. **Disbursement Reconciliation**
   - Auto-match disbursement to loan account
   - General ledger posting
   - Borrower notification (SMS, email, app)
   - Disbursement certificate generation

---

=====================================================================

## Page 3.7 — Loan Servicing & Account Administration

**Purpose:** Ongoing management of all active PayMo loans.

### Sections & Content:

1. **Loan Account Register**
   - Complete book of all active loans
   - Filters: product, status, risk grade, DPD, officer, branch
   - Columns: borrower, principal, interest accrued, total balance, next due date, DPD
   - Bulk actions: status update, rate change, restructuring flag

2. **Individual Loan Account Detail**
   - Borrower profile and contact info
   - Loan terms snapshot
   - Current balance: principal outstanding, interest accrued, fees, penalties
   - Full transaction history
   - Repayment schedule
   - Collateral summary
   - Communication log

3. **Interest & Fee Management**
   - Interest accrual engine (daily)
   - Calculation methods: flat, reducing balance, amortized
   - Interest rate type: fixed, floating (with reference rate)
   - Rate change processing
   - Fee posting: processing fee, late fee, prepayment penalty
   - Interest capitalization (for moratoriums)

4. **Repayment Schedule Engine**
   - Auto-generation upon disbursement
   - Schedule types: equal installments, bullet, seasonal, custom
   - Payment components: principal, interest, insurance premium, fees
   - Prepayment impact recalculation
   - Rescheduling upon restructuring

5. **Loan Status Management**
   - Active → Watchlist → Substandard → Doubtful → Loss → Closed → Written Off
   - Automatic status triggers (DPD, covenant breach)
   - Manual status override with approval
   - Write-off processing

---

## Page 3.8 — Collections & Recovery

**Purpose:** Structured collection of repayments and management of delinquent accounts.

### Sections & Content:

1. **Collections Dashboard**
   - Expected collections today/this week/this month
   - Actual collections vs. target
   - Collection rate by product, segment, officer
   - Aging analysis: current, 1-30, 31-60, 61-90, 90+ DPD
   - PAR 30, PAR 60, PAR 90 metrics

2. **Auto-Debit & Standing Orders**
   - Direct debit mandate management
   - Auto-debit scheduling (pre-due, on-due, post-due)
   - Failed debit handling and retry logic (3 attempts with escalation)
   - Mandate suspension and reactivation
   - Alternative payment method fallback

3. **Repayment Channels**
   - PayMo wallet deduction
   - Bank transfer to PayMo collection account
   - Mobile money (M-Pesa, etc.)
   - Card payment
   - Cash payment at agent/branch
   - Salary deduction (payroll integration)

4. **Delinquency Management Workflow**
   - **Stage 1 (1-30 DPD):** Automated reminders (SMS, email, app push), soft collection calls
   - **Stage 2 (31-60 DPD):** Formal demand letters, intensified calling, payment plan offer
   - **Stage 3 (61-90 DPD):** Legal notice, field visit scheduling, collateral reminder
   - **Stage 4 (90+ DPD):** Legal action initiation, collateral enforcement, write-off consideration
   - Task assignment to collections officers
   - Escalation rules and SLA

5. **Payment Plan & Restructuring**
   - Payment plan proposal generation
   - Term extension, rate reduction, principal holiday
   - Impact on NPV and expected recovery
   - Payment plan agreement documentation
   - Compliance monitoring post-restructure

6. **Recovery & Enforcement**
   - Collateral repossession workflow
   - Asset disposal and realization
   - Legal proceeding tracking
   - Recovery proceeds allocation
   - Shortfall recovery pursuit
   - Write-off approval and processing

---

## Page 3.9 — Collateral & Security Management

**Purpose:** Tracking and management of all security held by PayMo for its loans.

### Sections & Content:

1. **Collateral Register**
   - Complete inventory of pledged assets
   - Linked to loan account and borrower
   - Types: cash deposit, real estate, vehicle, equipment, securities, guarantee, receivables
   - Current market value and forced sale value
   - Loan-to-value (LTV) ratio tracking

2. **Real Estate Collateral**
   - Property details: address, title number, size, type
   - Valuation history (independent appraiser)
   - Title deed storage and verification
   - Mortgage/charge registration status
   - Insurance: fire, building, title
   - Property inspection schedule

3. **Movable Collateral**
   - Vehicle: registration, logbook, valuation, tracking device
   - Equipment: description, serial number, location, valuation
   - Securities: ISIN, quantity, market value, custodian
   - Receivables: debtor list, assignment notice, collection account

4. **Cash Collateral & Guarantees**
   - Fixed deposit lien status
   - Guarantee details: guarantor, amount, expiry
   - Insurance policy assignment
   - Letter of credit as collateral

5. **Collateral Monitoring**
   - LTV threshold alerts
   - Valuation review schedule
   - Insurance expiry tracking
   - Security perfection renewal
   - Collateral release upon loan closure

---

## Page 3.10 — Covenant Monitoring (Corporate & Real Estate)

**Purpose:** Tracking borrower compliance with loan agreement terms for larger facilities.

### Sections & Content:

1. **Covenant Dashboard**
   - All active covenants across corporate and real estate book
   - Compliance status: compliant, breached, waived, under review
   - Upcoming test dates
   - Historical trend

2. **Financial Covenant Testing**
   - Automated calculation from borrower-submitted financials
   - DSCR, leverage ratio, interest coverage, net worth
   - Actual vs. threshold comparison
   - Test documentation

3. **Information Covenant Tracking**
   - Required reporting: audited financials, management accounts, compliance certificates
   - Due dates and receipt status
   - Overdue alerts and follow-up

4. **Breach Management**
   - Breach alert and escalation
   - Remediation plan requirement
   - Waiver request and negotiation
   - Cross-default check

---

## Page 3.11 — Restructuring & Forbearance

**Purpose:** Managing distressed loans through workout and modification.

### Sections & Content:

1. **Distressed Loan Identification**
   - Early warning signals
   - DPD, covenant breach, rating downgrade triggers
   - Watchlist register

2. **Restructuring Options**
   - Term extension
   - Interest rate reduction
   - Principal repayment holiday
   - Partial principal forgiveness
   - Debt-to-equity conversion
   - Collateral substitution

3. **Forbearance Management**
   - Forbearance classification and measure
   - Period tracking and exit criteria
   - Regulatory reporting

4. **Provisioning & Write-Off**
   - IFRS 9 stage migration
   - Provision calculation and posting
   - Write-off approval workflow
   - Recovery tracking post-write-off

---

## Page 3.12 — Credit Analytics & Portfolio Intelligence

**Purpose:** Advanced analytics for PayMo's lending portfolio management.

### Sections & Content:

1. **Portfolio Quality**
   - NPL ratio, provision coverage
   - Stage migration analysis
   - Vintage analysis
   - Roll rate analysis

2. **Product Profitability**
   - Revenue: interest income, fees
   - Costs: cost of funds, provisions, operations, collections
   - Net margin per product
   - Customer lifetime value

3. **Predictive Analytics**
   - Early default warning
   - Optimal pricing
   - Collection prioritization
   - Cross-sell recommendations

4. **Stress Testing**
   - Macroeconomic scenarios
   - Portfolio impact modeling
   - Capital adequacy impact

---

## Page 3.13 — Capital & Funding Management

**Purpose:** Managing PayMo's capital deployment and funding sources for lending.

### Sections & Content:

1. **Capital Deployment**
   - Capital allocated vs. deployed
   - Utilization by product and segment
   - Return on deployed capital

2. **Funding Sources**
   - Equity capital
   - Warehouse facilities (bank lines)
   - Securitization programs
   - Bond issuances
   - Deposits (if licensed)

3. **Liquidity Planning**
   - Loan book maturity profile
   - Funding maturity profile
   - Asset-liability mismatch monitoring
   - Refinancing schedule

---

## Page 3.14 — Partner & Channel Management

**Purpose:** Managing third-party channels that originate loans for PayMo.

### Sections & Content:

1. **Partner Directory**
   - Merchants (BNPL partners)
   - Employers (payroll loan partners)
   - Real estate developers
   - Brokers and agents
   - Embedded finance API partners

2. **Partner Performance**
   - Volume originated per partner
   - Default rate per partner
   - Commission/fee per partner
   - Partner scorecard

3. **Commission Management**
   - Commission structure per partner
   - Commission calculation and accrual
   - Commission payment scheduling
   - Partner statement

---
==================================================================================================== xxxxxxxx not inlcuded
## dashboard 4 — Customer Self-Service Portal (Borrower-Facing)

**Purpose:** White-labeled portal for PayMo borrowers to manage their loans.

### Sections & Content:

1. **Loan Dashboard**
   - Active loans summary
   - Outstanding balance
   - Next payment due
   - Payment history

2. **Make a Payment**
   - One-time payment
   - Auto-debit setup
   - Payment method selection

3. **Loan Documents**
   - Agreement download
   - Statement download
   - Tax certificate

4. **Apply for Top-Up / New Loan**
   - Pre-approved offers
   - Quick application

5. **Support**
   - Chat support
   - Payment issues
   - Statement requests

---
============================================================================ xxxxxxxxx
## Cross-Dashboard Integration

| Integration Point | Dashboard 1 Action | Dashboard 3 Action |
|-------------------|-------------------|-------------------|
| Loan disbursement | Execute transfer to borrower account | Record disbursement, activate loan |
| Repayment collection | Process incoming payment | Post to loan account, update balance |
| Interest/fee payment | Schedule auto-debit | Confirm receipt, update accruals |
| FX loan | Cross-currency transfer | Record at functional currency |
| Collections via virtual account | Virtual account receives payment | Auto-allocate to loan |
| Insurance premium | Bill pay for collateral insurance | Confirm coverage maintained |

---

This revised Dashboard 3 positions PayMo as a **direct lender** with full control over the credit lifecycle, from origination through recovery — integrated seamlessly with your payment rails (Dashboard 1) and value-added services (Dashboard 2).

 # PayMo BaaS Fintech — Dashboard 3: PayMo Lending & Credit Services

** Architecture:** PayMo operates as the **lender of record** — originating, underwriting, disbursing, servicing, and collecting on loans and credit facilities directly to retail consumers, SMEs, corporates, and real estate developers. PayMo's balance sheet or funded warehouse lines are the source of capital. Dashboard 3 is the **internal credit operations center** for PayMo's lending business.

---

## Dashboard 3 Overview

**Purpose:** End-to-end lending operations for PayMo as a direct lender offering:
- **Retail Lending:** Personal loans, salary advances, buy-now-pay-later (BNPL), credit cards
- **SME & Business Lending:** Working capital, invoice financing, equipment loans, trade finance
- **Corporate Lending:** Term loans, revolving credit facilities, project finance
- **Real Estate Lending:** Construction finance, mortgage/home loans, commercial real estate (CRE)

**Capital Structure:** PayMo deploys its own capital, warehouse facilities, or securitization programs 

---

## Page 3.1 — Lending Command Center

**Purpose:** Real-time strategic and operational overview of PayMo's entire lending book.

### Sections & Content:

1. **Portfolio Snapshot**
   - Total gross loan book (outstanding principal)
   - Net loan book (after provisions)
   - Breakdown by product: Retail | SME | Corporate | Real Estate
   - Breakdown by currency
   - Month-over-month growth rate

2. **Live Origination & Collection Ticker**
   - New applications submitted (real-time)
   - Loans approved and disbursed today
   - Repayments received today
   - Defaults/recoveries today
   - Auto-refresh every 5 seconds

3. **Key Lending KPIs**
   - Disbursement volume (today / MTD / YTD)
   - Collection rate vs. target
   - Portfolio at Risk (PAR): PAR 30, PAR 60, PAR 90
   - Non-Performing Loan (NPL) ratio
   - Cost of Risk (provisions / average loans)
   - Net Interest Margin (NIM)
   - Return on Assets (ROA) for lending division

4. **Product Performance Grid**
   - Performance per product line:
     | Product | Book Size | Avg Ticket | PAR 30 | NPL | Yield |
   - Color-coded health indicators
   - Trend arrows (improving/deteriorating)

5. **Cash Flow & Liquidity for Lending**
   - Capital deployed vs. capital available
   - Warehouse facility utilization
   - Upcoming maturities (principal repayments due)
   - Securitization pipeline
   - Liquidity gap forecast (linked to Dashboard 1 nostro positions)

6. **Actionable Alerts Queue**
   - Loans approaching maturity (30/60/90 days)
   - PAR 30+ accounts requiring follow-up
   - Covenant breaches (corporate/real estate)
   - Insurance expiries on collateral
   - Valuation reviews due
   - Credit limit overruns

---

## Page 3.2 — Loan Products & Pricing Engine

**Purpose:** Configure, manage, and price all PayMo loan products.

### Sections & Content:

1. **Product Catalog**
   - **Retail Products:**
     - Personal Loan (unsecured)
     - Salary Advance / Payroll Loan
     - Buy Now Pay Later (BNPL) — merchant-integrated
     - Credit Card / Line of Credit
     - Education Loan
     - Medical Emergency Loan
     - Asset Finance (vehicle, electronics)
   - **SME Products:**
     - Working Capital Loan
     - Invoice Financing / Factoring
     - Purchase Order Financing
     - Equipment / Machinery Loan
     - Trade Finance (L/C, guarantees)
     - Merchant Cash Advance
   - **Corporate Products:**
     - Term Loan
     - Revolving Credit Facility
     - Overdraft Facility
     - Project Finance
     - Bridge Loan
     - Syndicated Loan (where PayMo is lead)
   - **Real Estate Products:**
     - Residential Mortgage / Home Loan
     - Construction Finance
     - Commercial Real Estate (CRE) Loan
     - Land Acquisition Loan
     - Refinancing / Top-up Loan

2. **Product Configuration**
   - Eligibility criteria per product
   - Min/max loan amounts
   - Tenor ranges
   - Interest rate structures: flat, reducing balance, fixed, floating
   - Fee structure: processing fee, commitment fee, late fee, prepayment penalty
   - Collateral requirements per tier
   - Insurance requirements
   - Grace period rules

3. **Pricing Engine**
   - Risk-based pricing matrix
   - Base rate + risk margin + liquidity margin + operational margin
   - Customer segment pricing (premium, standard, high-risk)
   - Promotional pricing campaigns
   - Competitive pricing benchmark
   - Minimum yield floor enforcement

4. **Product Performance Analytics**
   - Volume and value per product
   - Default rate per product
   - Profitability per product (revenue minus cost of funds, provisions, ops cost)
   - Customer acquisition cost per product
   - Cross-sell and upsell rates

---

## Page 3.3 — Application Intake & Pre-Screening

**Purpose:** Capture and initially evaluate all loan applications from consumers and businesses.

### Sections & Content:

1. **Application Channels**
   - **Retail:** Mobile app, web portal, USSD, agent network, merchant POS
   - **SME:** Business portal, relationship manager submission, API (embedded finance partners)
   - **Corporate:** Direct RM submission, treasury portal, API integration
   - **Real Estate:** Developer portal, broker submission, direct application

2. **Application Form Builder**
   - Dynamic forms per product type
   - Fields: personal/business details, loan amount, purpose, tenor, income/revenue
   - Document upload: ID, proof of address, bank statements, payslips, financials
   - Consent for credit bureau check and data processing
   - Digital signature capture

3. **Application Pipeline Board**
   - Stages: Submitted → Data Verification → Pre-screened → Underwriting → Approved → Declined → Cancelled
   - Volume and value at each stage
   - Conversion funnel analytics
   - SLA breach alerts per stage
   - Assigned officer display

4. **Automated Pre-Screening**
   - Eligibility rule engine check
   - Credit bureau score pull (real-time API)
   - Identity verification (KYC/KYB)
   - Fraud detection screening
   - Watchlist and sanctions screening
   - Existing exposure check (single borrower limit)
   - Pre-screen score and recommendation

5. **Application Scoring**
   - Application scorecard output
   - Risk grade assignment (A to F or 1 to 10)
   - Auto-approve threshold (low risk, small ticket)
   - Auto-decline threshold (high risk, policy breach)
   - Manual review queue (medium risk)

---

## Page 3.4 — Credit Underwriting & Decisioning

**Purpose:** Comprehensive risk assessment and credit decision-making for PayMo as lender.

### Sections & Content:

1. **Retail Underwriting**
   - **Income Verification:**
     - Bank statement analysis (auto-parse via open banking)
     - Payslip verification
     - Employment verification API
     - Alternative data: mobile money history, utility payments, rental history
   - **Debt Burden Analysis:**
     - Existing debt obligations (credit bureau + internal)
     - Debt-to-income (DTI) ratio calculation
     - Disposable income assessment
   - **Behavioral Scoring:**
     - Transaction pattern analysis
     - Account stability scoring
     - Social graph analysis (where permitted)
   - **Decision:** Approve / Decline / Refer with conditions / Counter-offer

2. **SME Underwriting**
   - **Business Financial Analysis:**
     - 2-3 year financial statement review
     - Bank statement analysis (6-12 months)
     - Cash flow cycle analysis
     - Revenue trend and seasonality
   - **Business Credit Assessment:**
     - Business credit score
     - Trade reference checks
     - Supplier/customer concentration
   - **Owner/Director Assessment:**
     - Personal credit check
     - Personal guarantee evaluation
     - Background and experience review
   - **Decision:** Approve / Decline / Conditional / Counter-offer

3. **Corporate Underwriting**
   - **Financial Statement Analysis:**
     - Audited financials (3 years)
     - Ratio analysis: DSCR, ICR, leverage, liquidity
     - Cash flow modeling and projections
     - Peer benchmarking
   - **Business Risk Assessment:**
     - Industry analysis and outlook
     - Competitive position
     - Management quality assessment
     - ESG risk evaluation
   - **Facility Structuring:**
     - Amount, tenor, repayment structure
     - Security/collateral requirements
     - Covenant package design
     - Pricing negotiation
   - **Decision:** Credit committee approval required

4. **Real Estate Underwriting**
   - **Project/Property Assessment:**
     - Property valuation (independent appraiser)
     - Location and market analysis
     - Developer track record (construction finance)
     - Building plans and permits verification
     - Environmental assessment
   - **Financial Viability:**
     - Project cost breakdown and feasibility
     - Sales/rental projections (market comparables)
     - Loan-to-value (LTV) calculation
     - Debt service coverage ratio (DSCR)
     - Pre-sales/commitment level (construction)
   - **Legal & Title:**
     - Title deed verification
     - Encumbrance search
     - Construction contract review
     - Insurance requirements
   - **Decision:** Real estate credit committee approval

5. **Credit Memo & Committee Workflow**
   - Auto-generated credit memorandum
   - Risk rating and recommendation
   - Digital approval workflow
   - Approval authority matrix (by amount, product, risk grade)
   - Minutes and decision record
   - Appeal process for declined applications

---

## Page 3.5 — Loan Documentation & Agreement Management

**Purpose:** Legal documentation generation, execution, and storage for PayMo loans.

### Sections & Content:

1. **Document Generation Engine**
   - **Retail:** Loan agreement, terms and conditions, direct debit mandate, disclosure statements
   - **SME:** Loan agreement, security documents, personal guarantee, board resolution
   - **Corporate:** Facility agreement, security trust deed, intercreditor agreement (if syndicated), legal opinion
   - **Real Estate:** Mortgage deed, charge over property, construction contract, insurance certificates, valuation report

2. **Dynamic Clause Library**
   - Standard clauses per product and jurisdiction
   - Variable insertion: borrower name, amount, rate, tenor, collateral description
   - Special conditions based on risk grade
   - Regulatory required disclosures
   - Version control and legal approval workflow

3. **E-Signature & Execution**
   - Digital signature workflow (DocuSign/Adobe Sign/HelloSign)
   - SMS OTP for retail customers
   - Witness and notarization requirements (where applicable)
   - Execution certificate generation
   - Document delivery to borrower

4. **Conditions Precedent (CP) Management**
   - CP checklist per product type
   - Status tracking: pending, received, verified, waived
   - Document upload and verification
   - CP satisfaction certificate
   - Loan activation trigger

5. **Document Repository**
   - Centralized storage with folder structure per borrower
   - Document expiration tracking (ID, insurance, valuation)
   - Renewal reminders
   - Audit trail of document access
   - Regulatory retention compliance

---

## Page 3.6 — Disbursement Management

**Purpose:** Controlled release of PayMo loan funds to approved borrowers.

### Sections & Content:

1. **Disbursement Queue**
   - Approved loans awaiting disbursement
   - CP completion status
   - Disbursement amount and account details
   - Priority ordering (urgent, standard)

2. **Disbursement Execution**
   - **Retail:** Direct to borrower's PayMo wallet or linked bank account
   - **SME:** To business operating account or supplier account (trade finance)
   - **Corporate:** To designated disbursement account per facility agreement
   - **Real Estate:** Staged disbursement to escrow or developer account tied to construction milestones
   - Payment rail selection (linked to Dashboard 1)
   - Disbursement confirmation and receipt

3. **Staged/Milestone Disbursement (Real Estate & Project Finance)**
   - Milestone definition and approval
   - Architect/engineer certification upload
   - Inspection report verification
   - Stage completion trigger
   - Partial disbursement execution
   - Cumulative disbursement tracking vs. total facility

4. **Disbursement Reconciliation**
   - Auto-match disbursement to loan account
   - General ledger posting
   - Borrower notification (SMS, email, app)
   - Disbursement certificate generation

---

=====================================================================

## Page 3.7 — Loan Servicing & Account Administration

**Purpose:** Ongoing management of all active PayMo loans.

### Sections & Content:

1. **Loan Account Register**
   - Complete book of all active loans
   - Filters: product, status, risk grade, DPD, officer, branch
   - Columns: borrower, principal, interest accrued, total balance, next due date, DPD
   - Bulk actions: status update, rate change, restructuring flag

2. **Individual Loan Account Detail**
   - Borrower profile and contact info
   - Loan terms snapshot
   - Current balance: principal outstanding, interest accrued, fees, penalties
   - Full transaction history
   - Repayment schedule
   - Collateral summary
   - Communication log

3. **Interest & Fee Management**
   - Interest accrual engine (daily)
   - Calculation methods: flat, reducing balance, amortized
   - Interest rate type: fixed, floating (with reference rate)
   - Rate change processing
   - Fee posting: processing fee, late fee, prepayment penalty
   - Interest capitalization (for moratoriums)

4. **Repayment Schedule Engine**
   - Auto-generation upon disbursement
   - Schedule types: equal installments, bullet, seasonal, custom
   - Payment components: principal, interest, insurance premium, fees
   - Prepayment impact recalculation
   - Rescheduling upon restructuring

5. **Loan Status Management**
   - Active → Watchlist → Substandard → Doubtful → Loss → Closed → Written Off
   - Automatic status triggers (DPD, covenant breach)
   - Manual status override with approval
   - Write-off processing

---

## Page 3.8 — Collections & Recovery

**Purpose:** Structured collection of repayments and management of delinquent accounts.

### Sections & Content:

1. **Collections Dashboard**
   - Expected collections today/this week/this month
   - Actual collections vs. target
   - Collection rate by product, segment, officer
   - Aging analysis: current, 1-30, 31-60, 61-90, 90+ DPD
   - PAR 30, PAR 60, PAR 90 metrics

2. **Auto-Debit & Standing Orders**
   - Direct debit mandate management
   - Auto-debit scheduling (pre-due, on-due, post-due)
   - Failed debit handling and retry logic (3 attempts with escalation)
   - Mandate suspension and reactivation
   - Alternative payment method fallback

3. **Repayment Channels**
   - PayMo wallet deduction
   - Bank transfer to PayMo collection account
   - Mobile money (M-Pesa, etc.)
   - Card payment
   - Cash payment at agent/branch
   - Salary deduction (payroll integration)

4. **Delinquency Management Workflow**
   - **Stage 1 (1-30 DPD):** Automated reminders (SMS, email, app push), soft collection calls
   - **Stage 2 (31-60 DPD):** Formal demand letters, intensified calling, payment plan offer
   - **Stage 3 (61-90 DPD):** Legal notice, field visit scheduling, collateral reminder
   - **Stage 4 (90+ DPD):** Legal action initiation, collateral enforcement, write-off consideration
   - Task assignment to collections officers
   - Escalation rules and SLA

5. **Payment Plan & Restructuring**
   - Payment plan proposal generation
   - Term extension, rate reduction, principal holiday
   - Impact on NPV and expected recovery
   - Payment plan agreement documentation
   - Compliance monitoring post-restructure

6. **Recovery & Enforcement**
   - Collateral repossession workflow
   - Asset disposal and realization
   - Legal proceeding tracking
   - Recovery proceeds allocation
   - Shortfall recovery pursuit
   - Write-off approval and processing

---

## Page 3.9 — Collateral & Security Management

**Purpose:** Tracking and management of all security held by PayMo for its loans.

### Sections & Content:

1. **Collateral Register**
   - Complete inventory of pledged assets
   - Linked to loan account and borrower
   - Types: cash deposit, real estate, vehicle, equipment, securities, guarantee, receivables
   - Current market value and forced sale value
   - Loan-to-value (LTV) ratio tracking

2. **Real Estate Collateral**
   - Property details: address, title number, size, type
   - Valuation history (independent appraiser)
   - Title deed storage and verification
   - Mortgage/charge registration status
   - Insurance: fire, building, title
   - Property inspection schedule

3. **Movable Collateral**
   - Vehicle: registration, logbook, valuation, tracking device
   - Equipment: description, serial number, location, valuation
   - Securities: ISIN, quantity, market value, custodian
   - Receivables: debtor list, assignment notice, collection account

4. **Cash Collateral & Guarantees**
   - Fixed deposit lien status
   - Guarantee details: guarantor, amount, expiry
   - Insurance policy assignment
   - Letter of credit as collateral

5. **Collateral Monitoring**
   - LTV threshold alerts
   - Valuation review schedule
   - Insurance expiry tracking
   - Security perfection renewal
   - Collateral release upon loan closure

---

## Page 3.10 — Covenant Monitoring (Corporate & Real Estate)

**Purpose:** Tracking borrower compliance with loan agreement terms for larger facilities.

### Sections & Content:

1. **Covenant Dashboard**
   - All active covenants across corporate and real estate book
   - Compliance status: compliant, breached, waived, under review
   - Upcoming test dates
   - Historical trend

2. **Financial Covenant Testing**
   - Automated calculation from borrower-submitted financials
   - DSCR, leverage ratio, interest coverage, net worth
   - Actual vs. threshold comparison
   - Test documentation

3. **Information Covenant Tracking**
   - Required reporting: audited financials, management accounts, compliance certificates
   - Due dates and receipt status
   - Overdue alerts and follow-up

4. **Breach Management**
   - Breach alert and escalation
   - Remediation plan requirement
   - Waiver request and negotiation
   - Cross-default check

---

## Page 3.11 — Restructuring & Forbearance

**Purpose:** Managing distressed loans through workout and modification.

### Sections & Content:

1. **Distressed Loan Identification**
   - Early warning signals
   - DPD, covenant breach, rating downgrade triggers
   - Watchlist register

2. **Restructuring Options**
   - Term extension
   - Interest rate reduction
   - Principal repayment holiday
   - Partial principal forgiveness
   - Debt-to-equity conversion
   - Collateral substitution

3. **Forbearance Management**
   - Forbearance classification and measure
   - Period tracking and exit criteria
   - Regulatory reporting

4. **Provisioning & Write-Off**
   - IFRS 9 stage migration
   - Provision calculation and posting
   - Write-off approval workflow
   - Recovery tracking post-write-off

---

## Page 3.12 — Credit Analytics & Portfolio Intelligence

**Purpose:** Advanced analytics for PayMo's lending portfolio management.

### Sections & Content:

1. **Portfolio Quality**
   - NPL ratio, provision coverage
   - Stage migration analysis
   - Vintage analysis
   - Roll rate analysis

2. **Product Profitability**
   - Revenue: interest income, fees
   - Costs: cost of funds, provisions, operations, collections
   - Net margin per product
   - Customer lifetime value

3. **Predictive Analytics**
   - Early default warning
   - Optimal pricing
   - Collection prioritization
   - Cross-sell recommendations

4. **Stress Testing**
   - Macroeconomic scenarios
   - Portfolio impact modeling
   - Capital adequacy impact

---

## Page 3.13 — Capital & Funding Management

**Purpose:** Managing PayMo's capital deployment and funding sources for lending.

### Sections & Content:

1. **Capital Deployment**
   - Capital allocated vs. deployed
   - Utilization by product and segment
   - Return on deployed capital

2. **Funding Sources**
   - Equity capital
   - Warehouse facilities (bank lines)
   - Securitization programs
   - Bond issuances
   - Deposits (if licensed)

3. **Liquidity Planning**
   - Loan book maturity profile
   - Funding maturity profile
   - Asset-liability mismatch monitoring
   - Refinancing schedule

---

## Page 3.14 — Partner & Channel Management

**Purpose:** Managing third-party channels that originate loans for PayMo.

### Sections & Content:

1. **Partner Directory**
   - Merchants (BNPL partners)
   - Employers (payroll loan partners)
   - Real estate developers
   - Brokers and agents
   - Embedded finance API partners

2. **Partner Performance**
   - Volume originated per partner
   - Default rate per partner
   - Commission/fee per partner
   - Partner scorecard

3. **Commission Management**
   - Commission structure per partner
   - Commission calculation and accrual
   - Commission payment scheduling
   - Partner statement

---
==================================================================================================== xxxxxxxx not inlcuded
## dashboard 4 — Customer Self-Service Portal (Borrower-Facing)

**Purpose:** White-labeled portal for PayMo borrowers to manage their loans.

### Sections & Content:

1. **Loan Dashboard**
   - Active loans summary
   - Outstanding balance
   - Next payment due
   - Payment history

2. **Make a Payment**
   - One-time payment
   - Auto-debit setup
   - Payment method selection

3. **Loan Documents**
   - Agreement download
   - Statement download
   - Tax certificate

4. **Apply for Top-Up / New Loan**
   - Pre-approved offers
   - Quick application

5. **Support**
   - Chat support
   - Payment issues
   - Statement requests

---
============================================================================ xxxxxxxxx
## Cross-Dashboard Integration

| Integration Point | Dashboard 1 Action | Dashboard 3 Action |
|-------------------|-------------------|-------------------|
| Loan disbursement | Execute transfer to borrower account | Record disbursement, activate loan |
| Repayment collection | Process incoming payment | Post to loan account, update balance |
| Interest/fee payment | Schedule auto-debit | Confirm receipt, update accruals |
| FX loan | Cross-currency transfer | Record at functional currency |
| Collections via virtual account | Virtual account receives payment | Auto-allocate to loan |
| Insurance premium | Bill pay for collateral insurance | Confirm coverage maintained |

---

This revised Dashboard 3 positions PayMo as a **direct lender** with full control over the credit lifecycle, from origination through recovery — integrated seamlessly with your payment rails (Dashboard 1) and value-added services (Dashboard 2).

chat history

The user wants me to create a comprehensive HTML page for "Page 1.4 — Payment Rails & Routing" following the same design patterns as the previous pages. This page is about payment infrastructure configuration and optimization.

Let me create a fully functional, responsive HTML page with:

Connected Banks Directory - list of banks with status, health, supported rails, etc.
Routing Rules Engine - smart routing configuration with rules
Rail Performance Analytics - charts/stats for success rates, settlement times, costs
Rail Configuration - enable/disable, limits, credentials, webhooks
Nostro/Vostro Account Mapping - balances, reconciliation, auto-sweep, FX
I'll use the same glassmorphism design, sidebar with anchor links, modals for actions, tabs for organization, and make it fully responsive.



in the same manner and design leaving no blanks, no dead ends, no placeholders, using modals, tabs popups relevantly and making it responsive
craete this page (.html)
Page 1.4 — Payment Rails & Routing
Purpose: Configuration and optimization of payment infrastructure.
Sections & Content:
Connected Banks Directory
List of all connected financial institutions
Connection status, API health, last sync time
Supported rails per bank
Settlement windows and cut-off times
Bank-specific limits and rules
Routing Rules Engine
Smart routing configuration
Rules by: amount threshold, currency, destination bank, urgency, cost ceiling
Fallback rail configuration
A/B testing for routing optimization
Rail Performance Analytics
Success rate per rail over time
Average settlement time per rail
Cost per transaction per rail
Failure reason analysis per rail
Rail Configuration
Enable/disable rails
Cut-off time management
Limit configuration (per transaction, daily, monthly)
Credential and certificate management
Webhook endpoint configuration per rail
Nostro/Vostro Account Mapping
Account balances per rail/currency
Reconciliation status
Auto-sweep rules
FX position management


The user wants me to create a complete HTML page for "Page 1.3 — Transfer Management" following the same design patterns as the previous pages. This page needs:

Advanced Filter Panel - with date range, amount range, currency, status filters, bank filters, rail filters, risk score filters, reference search
Transfers Data Table - sortable columns, row actions, bulk actions
Transfer Detail Drawer/Modal - full transfer journey timeline, status history, failure reasons, fees breakdown, reconciliation entries, audit trail
Exception Management - failed transfers, return items, compliance holds, retry mechanism
Bulk Operations Center - upload history, template downloads, bulk approval workflows, error reports
I need to:

Keep sidebar navs as anchor tags (not modals)
Use modals/tabs/popups where relevant
Make it fully responsive
No dead ends, no placeholders, no blanks
Same glassmorphism design as the other pages
Let me create a comprehensive page with:

Filter panel that's collapsible
Full data table with sample data
Detail modal/drawer with tabs for different sections
Exception management section
Bulk operations section
All interactive elements working

Created public/transfer-management.html


in the same manner and design leaving no blanks, no dead ends, no placeholders, using modals, tabs popups relevantly and making it responsive
create the .html for page 1.3
Page 1.3 — Transfer Management
Purpose: Complete lifecycle management of all transfers.
Sections & Content:
Advanced Filter Panel
Date range, amount range, currency
Status filter: Draft, Pending, Processing, Completed, Failed, Cancelled, Returned
Sender/receiver bank filter
Payment rail filter
Risk score filter
Reference number search
Transfers Data Table
Sortable columns: ID, date, amount, sender, receiver, rail, status, risk score
Row actions: View details, Edit (if draft), Cancel, Clone, Download receipt
Bulk actions: Approve, Reject, Export
Transfer Detail Drawer/Modal
Full transfer journey timeline (initiated → authorized → processed → settled)
Status history with timestamps
Failure reason (if failed) with retry options
Associated fees breakdown
Linked reconciliation entries
Audit trail (who did what when)
Exception Management
Failed transfers requiring investigation
Return items (R01, R02, R03 return reason codes)
Compliance holds with resolution actions
Retry mechanism with configurable rules
Bulk Operations Center
Upload history and status
Template downloads (CSV, XML, ISO 20022)
Bulk approval workflows
Error report downloads

The user wants me to create a single combined HTML page for "Page 1.2 — Initiate Transfer" in the same style as the dashboard I just built. Key requirements:

Same glassmorphism design style
Sidebar navigation should use blank anchor tags (href="#") NOT modals
All sections from the spec should be fully populated - no blanks, no dead ends
Responsive design
Modals where relevant for forms/selections
Single self-contained HTML file
Let me build this comprehensive transfer initiation page with all the sections:

Transfer Type Selector - tabs/cards for Single, Bulk, Recurring, Instant vs Standard
Sender Details - source account dropdown, balance, verification status
Receiver Details - bank search, account input with validation, name verification, save to address book
Transfer Amount & Currency - amount input, currency selector, FX rate, fee breakdown
Payment Rail Selection - smart routing recommendation, rail options with time/cost
Transfer Purpose & Compliance - purpose code, reference, document upload, priority
Authorization Workflow - approval chain, 2FA, scheduled time
Transfer Summary & Confirmation - review, terms, submit
I'll use modals for:

Bank selection (search directory)
Document upload
FX rate details
Approval chain details
Terms & conditions
Success confirmation
The sidebar will have the same structure but with href="#" anchor links instead of onclick modals.


Created public/initiate-transfer.html


in the same manner leaving no blanks build html for page 1.2
side bar navs should remian blank url anchor tags not modals

Page 1.2 — Initiate Transfer
Purpose: Single and bulk transfer creation with intelligent routing.
Sections & Content:
Transfer Type Selector
Single transfer
Bulk/batch transfer (CSV/Excel upload)
Recurring/scheduled transfer
Instant vs. standard settlement
Sender Details
Source account selection (nostro, float, client account)
Available balance display
Account verification status
Receiver Details
Bank search & selection (connected institutions directory)
Account number / IBAN input with validation
Account name verification (name matching API)
Beneficiary save to address book toggle
Transfer Amount & Currency
Amount input with currency selector
Real-time FX rate display (if cross-currency)
Fee breakdown: platform fee, bank fee, FX spread
Total debit amount preview
Payment Rail Selection
Smart routing recommendation (fastest/cheapest/balanced)
Rail options: ACH, SEPA, SWIFT, Wire, FPS, PesaLink, Real-time
Estimated settlement time per rail
Cost comparison per rail
Transfer Purpose & Compliance
Purpose code selection (salary, invoice, dividend, loan, etc.)
Reference/narration field
Supporting document upload (invoice, contract)
Priority flag (normal/urgent/critical)
Authorization Workflow
Approval chain preview (maker-checker-approver)
Digital signature / 2FA requirement
Scheduled execution time picker
Transfer Summary & Confirmation
Full transfer details review
Terms and conditions acceptance
Confirm & submit button




 # PayMo BaaS Fintech — Complete Platform Architecture Outline

Based on deep research into PesaLink, Plaid, Payoneer, and leading 2026 BaaS platforms (Gemba, Solaris, SDK.finance, Marqeta, Galileo, Azify), here is a comprehensive, production-grade outline for your PayMo BaaS fintech platform.

---

## Platform Overview

**PayMo** is a Banking-as-a-Service (BaaS) platform that provides financial infrastructure for bank-to-bank transfers, cash flow management, and value-added financial services. The platform is split into two primary dashboards:

| Dashboard | Purpose |
|-----------|---------|
| **Dashboard 1: Bank-to-Bank Transactions** | Core payment rails, transfer orchestration, liquidity management, and transaction lifecycle |
| **Dashboard 2: Bank-to-Bank Services & Utilities** | Value-added services built on top of the transfer infrastructure — billing, collections, FX, compliance, analytics |

---



---

# PayMo BaaS Fintech — Dashboard 1: Bank-to-Bank Transactions (Africa-First Edition)

**Architecture Principle:** PayMo is built **Africa-first, globally-ready**. The default experience is optimized for Kenyan, East African, and broader African markets — with M-Pesa, PesaLink, RTGS, mobile money interoperability, and local PSPs as first-class citizens. Global rails (SWIFT, SEPA, ACH, PayPal, etc.) are fully supported but layered on top of the local foundation.

---

## Page 1.1 — Transfer Overview (Command Center)

**Purpose:** Real-time operational command center for all money movement across local African rails, mobile money, and global payment infrastructure.

### Section 1.1.1 — Live Transaction Ticker

- **Real-time feed** of all incoming and outgoing transactions across every rail
- **Per-transaction display:** Amount, currency (KES/UGX/TZS/RWF/USD/EUR/GBP), sender identifier (bank name / M-Pesa number / PayPal email / MTN MoMo), receiver identifier, payment rail used, transaction status, exact timestamp (EAT/CAT/WAT/GMT), and transaction reference
- **Color-coded status indicators:** Green (completed), Amber (processing/pending), Red (failed), Blue (scheduled), Purple (reversed)
- **Auto-refresh every 3 seconds** with WebSocket push notifications
- **Sound alerts** for high-value transactions (configurable threshold per currency)
- **Filter ticker by:** Rail type, currency, amount range, sender category, receiver category, risk flag
- **Click-to-drill:** Any ticker item expands to full transaction detail drawer
- **Export ticker snapshot** to CSV/Excel for the last 1,000 transactions
- **Transaction volume sparkline** next to each active rail showing last 60 minutes of activity

### Section 1.1.2 — Multi-Currency Performance Metrics (KPIs)

- **Total volume today / this week / this month / this quarter** with currency breakdown
  - KES (Kenyan Shilling) — primary operating currency
  - UGX (Ugandan Shilling)
  - TZS (Tanzanian Shilling)
  - RWF (Rwandan Franc)
  - NGN (Nigerian Naira)
  - GHS (Ghanaian Cedi)
  - ZAR (South African Rand)
  - USD (US Dollar)
  - EUR (Euro)
  - GBP (British Pound)
- **Transaction success rate** per rail with target thresholds:
  - M-Pesa: 99.5%+
  - PesaLink: 99.2%+
  - RTGS: 99.8%+
  - EFT: 98.5%+
  - SWIFT: 97.0%+
  - Mobile Money Interoperability: 98.0%+
- **Average settlement time** per rail:
  - M-Pesa STK Push: < 10 seconds
  - PesaLink: < 7 seconds
  - RTGS: Real-time (banking hours)
  - EFT: T+1 to T+3
  - SWIFT: T+1 to T+5
  - PAPSS: < 120 seconds
- **Active payment rails count** with health status
- **Failed transactions requiring attention** with auto-prioritization by value and age
- **Revenue generated** today from transaction fees, FX spreads, and rail commissions
- **Cost per transaction** per rail for margin analysis
- **Customer satisfaction score** (CSAT) from post-transaction surveys

### Section 1.1.3 — African Payment Rail Status Grid

- **M-Pesa (Safaricom):**
  - Real-time health: API response time, Daraja portal status, STK Push success rate
  - Daily transaction volume vs. capacity
  - B2C disbursement queue status
  - C2B collection queue status
  - Settlement window: T+0 for merchant tiers
  - Maintenance windows (Safaricom scheduled downtime)
  - Agent network liquidity alerts
- **PesaLink (IPSL):**
  - Interbank switch status
  - Connected bank count (30+ Kenyan banks)
  - Transaction throughput per second
  - Mobile-number-to-bank linkage health
  - 24/7 uptime indicator
  - Per-bank connection status (KCB, Equity, Co-op, Stanbic, ABSA, NCBA, DTB, etc.)
- **RTGS (CBK):**
  - Kenya Electronic Payment and Settlement System (KEPSS) status
  - Settlement queue depth
  - Cut-off time countdown (typically 3:00 PM EAT)
  - Next business day preview
  - High-value transaction threshold (KES 1,000,000+)
- **EFT (ACH):**
  - Batch processing schedule
  - Current batch status
  - Expected settlement timeline
  - File format validation status (ISO 20022, CSV)
- **Mobile Money Interoperability:**
  - M-Pesa ↔ Airtel Money rail status
  - M-Pesa ↔ T-Kash rail status
  - Airtel Money ↔ T-Kash rail status
  - Cross-network transaction success rate
  - Interoperability settlement reconciliation status
- **East Africa Payment System (EAPS):**
  - Cross-border East African Community rail status
  - Connected central banks: CBK, BoU, BoT, NBR, CBS
  - EAPS transaction volume and value
- **PAPSS (Pan-African Payment and Settlement System):**
  - Cross-African rail status
  - Connected countries and currencies
  - Pre-funding account balances per participant
  - Settlement in local currencies vs. hard currencies
- **Global Rails:**
  - SWIFT gpi status and tracker availability
  - SEPA Instant status
  - ACH (US) status
  - FPS (UK Faster Payments) status
  - PayPal API status
  - Visa Direct / Mastercard Send status

### Section 1.1.4 — Multi-Currency Liquidity Position Summary

- **Real-time balances across all nostro accounts and float accounts:**
  - KES float at Safaricom (M-Pesa)
  - KES nostro at KCB, Equity, Co-op, Stanbic
  - USD nostro at correspondent banks
  - EUR nostro at correspondent banks
  - GBP nostro at correspondent banks
  - UGX float at MTN Uganda / Airtel Uganda
  - TZS float at Vodacom Tanzania / Airtel Tanzania
  - Regional currency positions for EAPS and PAPSS
- **Low-balance alerts** per account with configurable thresholds
- **Auto-replenishment triggers** and rules configuration
- **FX position summary:** Net exposure per currency pair
- **Intraday liquidity forecast** based on scheduled disbursements and expected collections
- **Concentration risk alerts** (over-reliance on single bank or currency)
- **Regulatory liquidity ratio monitoring** (CBK requirements for Kenyan operations)

### Section 1.1.5 — Pending Actions Queue

- **Compliance holds:** Transactions flagged by AML engine awaiting manual review
- **KRA eTIMS integration holds:** Transactions requiring tax invoice verification before release
- **High-value approval queue:** Transactions exceeding single-approver limit requiring second authorization
- **Exception items:** Failed M-Pesa STK Push retries, reversed PesaLink transactions, RTGS rejections
- **SLA breach warnings:** Transactions approaching or exceeding service level agreements
- **Bulk upload errors:** Failed batch transactions with error detail and correction suggestions
- **Reconciliation mismatches:** Unmatched items from bank statements requiring investigation

### Section 1.1.6 — Quick Action Bar

- **Initiate new transfer** — single, bulk, or scheduled
- **M-Pesa STK Push** — quick send payment request to customer phone
- **B2C disbursement** — quick send money to M-Pesa mobile number
- **Bulk upload transfers** — CSV/Excel upload with template download
- **Schedule recurring transfer** — standing order setup
- **Generate instant report** — pre-configured report templates
- **Emergency liquidity request** — trigger nostro funding from partner bank
- **Switch currency view** — toggle primary display currency (KES default, with USD/EUR/UGX/TZS quick-switch)

---

## Page 1.2 — Initiate Transfer

**Purpose:** Single, bulk, and scheduled transfer creation with intelligent routing optimized for African and global corridors.

### Section 1.2.1 — Transfer Type Selector

- **Single transfer** — one-time payment to single beneficiary
- **Bulk/batch transfer** — CSV/Excel upload supporting:
  - M-Pesa B2C bulk disbursements (salary payments, supplier payments)
  - PesaLink bulk transfers
  - RTGS batch files
  - EFT payroll files
  - Mixed-rail bulk (some M-Pesa, some bank transfer)
- **Recurring/scheduled transfer** — standing orders with:
  - Daily, weekly, bi-weekly, monthly, quarterly, annual frequency
  - End date or number of occurrences
  - Skip weekend/holiday rules (next business day, previous business day, exact date)
  - Kenyan public holiday calendar (Madaraka Day, Mashujaa Day, Jamhuri Day, etc.)
  - East African public holidays
  - Global holiday calendars per currency jurisdiction
- **Instant vs. standard settlement** — urgency-based rail selection
- **Cross-border vs. domestic** — corridor classification with regulatory pre-checks
- **Currency-specific transfer types:**
  - KES domestic (PesaLink, RTGS, EFT, M-Pesa)
  - KES↔UGX (EAPS, mobile money)
  - KES↔TZS (EAPS, mobile money)
  - KES↔USD (SWIFT, correspondent banking)
  - USD domestic (ACH, Wire)
  - EUR domestic (SEPA, SEPA Instant)

### Section 1.2.2 — Sender Details

- **Source account selection:**
  - PayMo KES float account (M-Pesa business account)
  - PayMo KES nostro at KCB / Equity / Co-op / Stanbic
  - PayMo USD nostro at correspondent bank
  - PayMo EUR nostro
  - PayMo UGX float (MTN/Airtel Uganda)
  - PayMo TZS float (Vodacom/Airtel Tanzania)
  - Client segregated accounts (for BaaS white-label clients)
- **Available balance display** in selected currency with real-time update
- **Account verification status:** Active, frozen, pending KYC, restricted
- **Daily/weekly/monthly transaction limits** per account with remaining capacity
- **Cost of funds indicator:** Interest cost if drawing on credit line, opportunity cost if using own funds

### Section 1.2.3 — Receiver Details

- **Beneficiary type selector:**
  - **Bank account** (Kenyan bank, East African bank, African bank, global bank)
  - **Mobile money wallet** (M-Pesa, Airtel Money, T-Kash, MTN MoMo, Orange Money)
  - **PayPal account** (email-based)
  - **Card** (Visa/Mastercard push-to-card)
  - **Digital wallet** (PayMo wallet, partner wallet)
- **Bank search & selection:**
  - Kenyan banks directory: KCB, Equity Bank, Co-operative Bank, Stanbic Bank, ABSA Bank Kenya, NCBA Bank, Diamond Trust Bank (DTB), I&M Bank, Standard Chartered, CitiBank, Barclays (legacy), Family Bank, SBM Bank, Guardian Bank, Gulf African Bank, First Community Bank, Habib Bank, Bank of Africa, Credit Bank, Consolidated Bank, Development Bank of Kenya, Ecobank, Fidelity Commercial Bank, Giro Commercial Bank, Guaranty Trust Bank, Habib Bank AG Zurich, Housing Finance, Imperial Bank (in receivership), Jamii Bora Bank, Kenya Commercial Bank (KCB), Middle East Bank, National Bank of Kenya, NIC Bank (merged), Oriental Commercial Bank, Paramount Universal Bank, Prime Bank, Spire Bank, Transnational Bank, UBA Kenya, Victoria Commercial Bank
  - East African banks: Bank of Uganda, Bank of Tanzania, National Bank of Rwanda, Bank of South Sudan
  - Major African banks: Standard Bank (South Africa), First Bank of Nigeria, Ecobank Transnational, Attijariwafa Bank, Banque Misr
  - Global banks: JP Morgan Chase, Citibank, HSBC, Barclays UK, Deutsche Bank, BNP Paribas
- **Account number / IBAN input with validation:**
  - Kenyan bank account format validation (varies by bank: some use 10 digits, some 12, some 14)
  - IBAN validation for international transfers
  - Mobile number validation for M-Pesa (2547XXXXXXXX format)
  - PayPal email format validation
- **Account name verification (name matching API):**
  - PesaLink name lookup by mobile number or account number
  - M-Pesa name lookup by phone number
  - Bank API name verification (where available)
  - Fuzzy matching with confidence score
  - Mismatch alert with override option (requires elevated approval)
- **Beneficiary save to address book toggle** with nickname and category tags (supplier, employee, customer, partner)

### Section 1.2.4 — Transfer Amount & Currency

- **Amount input with currency selector:**
  - Default: KES (Kenyan Shilling)
  - Quick-switch: UGX, TZS, RWF, NGN, GHS, ZAR, USD, EUR, GBP, CNY, JPY
  - Multi-currency display: show equivalent in 2-3 other currencies simultaneously
- **Real-time FX rate display** (if cross-currency):
  - Mid-market rate from central bank or Reuters
  - PayMo spread applied
  - Customer rate vs. interbank rate comparison
  - Rate lock duration (15 minutes, 1 hour, 24 hours)
  - Rate alert: notify if rate moves favorably before execution
- **Fee breakdown:**
  - Platform fee (PayMo margin)
  - Rail fee (M-Pesa, PesaLink, RTGS, SWIFT, etc.)
  - FX spread (if applicable)
  - Correspondent bank fee (for SWIFT)
  - Regulatory levy (where applicable, e.g., CBK levy)
  - **Total all-in cost** and **effective cost percentage**
- **Total debit amount preview** from source account including all fees

### Section 1.2.5 — Payment Rail Selection

- **Smart routing recommendation engine:**
  - **Fastest:** Prioritizes speed (M-Pesa STK Push, PesaLink, SEPA Instant)
  - **Cheapest:** Prioritizes lowest total cost (EFT, mobile money interoperability)
  - **Balanced:** Optimizes for speed-cost ratio (PesaLink for KES, SWIFT gpi for USD)
  - **Most Reliable:** Prioritizes highest success rate rail
  - **Regulatory Compliant:** Ensures chosen rail meets transaction purpose requirements
- **Rail options with detailed comparison:**
  - **M-Pesa STK Push:** Best for KES < KES 150,000 to mobile wallets. Settlement: T+0. Fee: 0.5-1.5%. Speed: < 10 seconds.
  - **M-Pesa B2C:** Best for disbursements to M-Pesa wallets. Settlement: T+0. Fee: tiered. Speed: < 30 seconds.
  - **M-Pesa C2B (Paybill/Till):** Best for collections. Settlement: T+0. Fee: merchant discount rate.
  - **PesaLink:** Best for KES interbank transfers KES 10 - KES 999,999. Settlement: Instant 24/7. Fee: KES 0 - KES 250. Speed: < 7 seconds.
  - **PesaLink to Mobile:** Send to mobile number linked to bank account. Settlement: Instant. Fee: KES 0 - KES 100.
  - **RTGS (KEPSS):** Best for KES ≥ KES 1,000,000. Settlement: Real-time (banking hours). Fee: KES 300 - KES 1,000+. Speed: Immediate.
  - **EFT (ACH):** Best for KES batch payments. Settlement: T+1 to T+3. Fee: KES 30 - KES 150. Speed: 1-3 days.
  - **Mobile Money Interoperability:** Cross-network M-Pesa ↔ Airtel Money ↔ T-Kash. Settlement: Near-instant. Fee: network-dependent.
  - **EAPS (East Africa Payment System):** Cross-border EAC transfers. Settlement: Same day. Fee: corridor-dependent.
  - **PAPSS:** Cross-African transfers in local currencies. Settlement: < 120 seconds. Fee: pre-funded.
  - **SWIFT gpi:** International transfers. Settlement: T+1 to T+5. Fee: USD 15 - USD 50+. Speed: 1-5 days.
  - **SEPA / SEPA Instant:** EUR transfers within EU. Settlement: Instant (SEPA Instant) or T+1 (SEPA). Fee: EUR 0 - EUR 5.
  - **ACH (US):** USD domestic transfers. Settlement: T+1 to T+3. Fee: USD 0.25 - USD 5.
  - **FPS (UK Faster Payments):** GBP domestic transfers. Settlement: Instant. Fee: GBP 0 - GBP 5.
  - **PayPal:** Global digital transfers. Settlement: Instant to PayPal, 1-3 days to bank. Fee: 2.9% + fixed.
  - **Visa Direct / Mastercard Send:** Card push payments. Settlement: < 30 minutes. Fee: 1-2%.
- **Estimated settlement time per rail** with confidence interval
- **Cost comparison per rail** with savings highlight
- **Rail availability check:** Is the rail currently operational? (banking hours, maintenance window, holiday)

### Section 1.2.6 — Transfer Purpose & Compliance

- **Purpose code selection (aligned with CBK and global standards):**
  - Salary / Payroll payment
  - Supplier / Vendor payment
  - Dividend distribution
  - Loan disbursement / repayment
  - Invoice payment
  - Tax payment (KRA iTax, GavaConnect)
  - Rent / Lease payment
  - Insurance premium
  - Utility bill payment
  - School fees / Education
  - Medical / Healthcare
  - Travel / Tourism
  - Family support / Remittance
  - Investment / Securities purchase
  - Donation / Charity
  - Government payment (G2P, P2G)
  - Other (requires description)
- **Reference/narration field** with character limit and auto-suggestions based on purpose
- **Supporting document upload:**
  - Invoice (PDF, image)
  - Purchase order
  - Contract agreement
  - KRA eTIMS tax invoice (auto-linked)
  - Board resolution (for corporate payments)
  - Beneficiary KYC document
- **Priority flag:** Normal / Urgent / Critical (affects routing and SLA)
- **Regulatory pre-checks:**
  - Sanctions screening (OFAC, UN, EU, local lists)
  - PEP screening
  - Single transaction limit check
  - Daily aggregate limit check
  - KRA tax compliance verification (for business payments)

### Section 1.2.7 — Authorization Workflow

- **Approval chain preview** based on amount and risk:
  - < KES 100,000: Single approver
  - KES 100,000 - KES 1,000,000: Maker + Checker
  - KES 1,000,000 - KES 10,000,000: Maker + Checker + Manager
  - > KES 10,000,000: Maker + Checker + Manager + Director + Compliance
  - Equivalent thresholds in USD, EUR, and other currencies
- **Digital signature / 2FA requirement:**
  - SMS OTP to registered mobile
  - Email OTP
  - Authenticator app (Google Authenticator, Authy)
  - Biometric approval (fingerprint, Face ID)
  - Hardware token (for highest values)
- **Scheduled execution time picker:**
  - Execute immediately
  - Schedule for specific date and time
  - Schedule for next business day
  - Schedule for end of month (salary payments)
  - Recurring schedule setup

### Section 1.2.8 — Transfer Summary & Confirmation

- **Full transfer details review** in printable format
- **Fee breakdown** with regulatory disclosure
- **FX rate lock confirmation** (if cross-currency)
- **Estimated settlement time** with tracking link preview
- **Terms and conditions acceptance** with specific rail terms
- **CBK regulatory disclosure** for Kenyan transactions
- **Data Protection Act 2019** consent confirmation
- **Confirm & submit button** with 5-second cooldown to prevent double-submit
- **Post-submission:** Transaction reference generation, QR code for tracking, shareable link

---

## Page 1.3 — Transfer Management

**Purpose:** Complete lifecycle management of all transfers across African and global rails.

### Section 1.3.1 — Advanced Filter Panel

- **Date range selector:** Today, Yesterday, Last 7 days, Last 30 days, Custom range, Fiscal quarter
- **Amount range:** Min/max with currency selector
- **Currency filter:** KES, UGX, TZS, RWF, NGN, GHS, ZAR, USD, EUR, GBP, and all supported currencies
- **Status filter:** Draft, Pending, Processing, Completed, Failed, Cancelled, Returned, Reversed, On Hold
- **Sender category:** PayMo float, PayMo nostro, Client account, Partner bank
- **Receiver category:** Kenyan bank, East African bank, African bank, Global bank, M-Pesa wallet, Airtel Money wallet, T-Kash wallet, MTN MoMo wallet, PayPal account, Card, Digital wallet
- **Payment rail filter:** M-Pesa STK Push, M-Pesa B2C, M-Pesa C2B, PesaLink, PesaLink to Mobile, RTGS, EFT, Mobile Money Interoperability, EAPS, PAPSS, SWIFT, SEPA, ACH, FPS, PayPal, Visa Direct, Mastercard Send
- **Risk score filter:** Low (1-3), Medium (4-6), High (7-10)
- **Purpose code filter:** All 20+ purpose categories
- **Reference number search:** Exact match and fuzzy search
- **Beneficiary name search:** Partial match
- **Mobile number search:** For M-Pesa and mobile money transactions
- **Transaction ID search:** Internal and external reference numbers
- **Compliance flag filter:** Sanctions hit, PEP hit, AML alert, KRA hold, manual review
- **Saved filter presets:** "Today's M-Pesa Disbursements," "Failed SWIFT Transfers," "High-Value RTGS," etc.

### Section 1.3.2 — Transfers Data Table

- **Sortable columns:** ID, Date/Time, Amount, Currency, Sender, Receiver, Rail, Status, Risk Score, Purpose, Reference, Officer
- **Column customization:** Show/hide columns, reorder, resize, pin columns
- **Row actions per transaction:**
  - View details (opens detail drawer)
  - Edit (if in Draft status)
  - Cancel (if Pending or Scheduled)
  - Clone (duplicate transaction with editable fields)
  - Download receipt (PDF with QR code)
  - Resend notification (SMS/email to beneficiary)
  - Reverse (if eligible per rail rules)
  - Escalate (send to compliance team)
  - Add note (internal memo)
- **Bulk actions:**
  - Approve multiple (for pending approvals)
  - Reject multiple
  - Export selected to CSV/Excel/PDF
  - Bulk reschedule
  - Bulk cancel
- **Pagination:** 25/50/100/500 rows per page
- **Infinite scroll option** for high-volume views
- **Export full dataset** (up to 100,000 rows) to Excel with formatting

### Section 1.3.3 — Transfer Detail Drawer/Modal

- **Transaction header:** Amount, currency, status badge, priority flag, risk score
- **Full transfer journey timeline:**
  - Initiated → Data Validation → Compliance Screening → Authorized → Submitted to Rail → Acknowledged by Rail → Processed → Settled → Confirmed → Completed
  - Each stage with timestamp, duration, and responsible system/user
  - Visual progress bar with current stage highlighted
- **Status history with timestamps:**
  - Every status change with reason code
  - User who triggered the change
  - System-triggered vs. manual changes
- **Failure reason (if failed):**
  - M-Pesa error codes: 0 (success), 1 (insufficient balance), 2001 (wrong PIN), 1032 (cancelled), 1037 (timeout), 500.001.1001 (insufficient business funds), 201 (unable to lock subscriber), 202 (subscriber not found), 400.002.02 (invalid amount), 400.002.03 (invalid payment type), 401.002.01 (unauthorized)
  - PesaLink error codes
  - RTGS rejection reasons
  - SWIFT MT nack codes
  - EFT return reason codes (R01-R85)
  - Retry options with suggested corrections
- **Associated fees breakdown:**
  - Platform fee
  - Rail fee
  - FX spread (if applicable)
  - Correspondent bank fee
  - Regulatory levy
  - Total cost
- **Linked reconciliation entries:**
  - Bank statement line item match
  - M-Pesa statement match
  - General ledger posting reference
  - Reconciliation status: Matched, Unmatched, Partially Matched
- **Audit trail:**
  - Who created the transaction
  - Who approved each stage
  - Who modified and when
  - Who cancelled/reversed and why
  - IP address and device fingerprint for each action
  - Immutable hash for tamper-proofing

### Section 1.3.4 — Exception Management

- **Failed transfers requiring investigation:**
  - Categorized by failure type: Insufficient funds, Invalid account, Network timeout, Compliance block, Rail downtime, System error
  - Auto-assignment to operations team based on category
  - SLA timer for resolution
- **Return items:**
  - EFT return reason codes: R01 (Insufficient funds), R02 (Account closed), R03 (No account), R04 (Invalid account number), R05 (Unauthorized debit), R06 (Returned per ODFI request), R07 (Authorization revoked), R08 (Payment stopped), R09 (Uncollected funds), R10 (Customer advises not authorized), R11 (Check truncation entry return), R12 (Branch sold to another DFI), R13 (RDFI not qualified), R14 (Representative payee deceased), R15 (Beneficiary deceased), R16 (Account frozen), R17 (File record edit criteria), R18 (Improper effective entry date), R19 (Amount field error), R20 (Non-transaction account), R21 (Invalid company identification), R22 (Invalid individual ID number), R23 (Credit entry refused), R24 (Duplicate entry), R25 (Addenda error), R26 (Mandatory field error), R27 (Trace number error), R28 (Routing number check digit error), R29 (Corporate customer advises not authorized), R30 (RDFI not participant in check truncation program), R31 (Permissible return entry), R32 (RDFI non-settlement), R33 (Return of XCK entry), R34 (Limited participation DFI), R35 (Return of improper debit entry), R36 (Return of improper credit entry), R37 (Source document presented for payment), R38 (Stop payment on source document), R39 (Improper source document), R40 (Return of ENR entry), R41 (Invalid transaction code), R42 (Routing number error), R43 (Invalid DFI account number), R44 (Invalid individual ID number), R45 (Invalid individual name), R46 (Invalid representative payee indicator), R47 (Duplicate return), R48 (Improper return), R49 (Item related to R10), R50 (Item related to R11), R51 (Item related to R29), R52 (Stop payment on item), R53 (Item and ACH entry presented for payment), R54 (Representative payee deceased), R55 (Beneficiary deceased), R56 (Return of improper debit), R57 (Return of improper credit), R58 (Return of XCK entry), R59 (Return of improper debit entry), R60 (Return of improper credit entry), R61 (Misrouted return), R62 (Return of erroneous debit), R63 (Return of erroneous credit), R64 (Return of erroneous reversal debit), R65 (Return of erroneous reversal credit), R66 (Return of erroneous credit), R67 (Return of erroneous debit), R68 (Return of erroneous reversal), R69 (Field error), R70 (Permissible return entry), R71 (Misrouted dishonored return), R72 (Untimely return), R73 (Timely original return), R74 (Corrected return), R75 (Return not accepted), R76 (No errors found), R77 (Non-acceptance of R62-R67), R78 (Improper reversal), R79 (Improper return), R80 (Cross-border return), R81 (International ACH return), R82 (Return of debit entry), R83 (Return of credit entry), R84 (Entry refused by receiver), R85 (Return of improper debit entry)
  - SWIFT return codes
  - M-Pesa reversal codes
- **Compliance holds with resolution actions:**
  - Sanctions hit: Review hit details, request waiver, reject transaction
  - PEP hit: Enhanced due diligence, senior approval, reject
  - AML alert: Investigation, SAR filing, freeze funds
  - KRA hold: Verify eTIMS invoice, request taxpayer PIN, release or reject
- **Retry mechanism with configurable rules:**
  - Auto-retry count: 0-5 attempts
  - Retry interval: Immediate, 5 min, 15 min, 1 hour, 4 hours, next business day
  - Escalation after max retries: Notify operations, notify beneficiary, cancel transaction
  - Smart retry: Switch to alternative rail on failure (e.g., PesaLink fails → try RTGS)

### Section 1.3.5 — Bulk Operations Center

- **Upload history and status:**
  - List of all bulk uploads with date, file name, row count, success count, fail count, status
  - Upload source: Web UI, API, SFTP, email attachment
- **Template downloads:**
  - M-Pesa B2C bulk template (CSV with phone number, amount, narrative columns)
  - PesaLink bulk template (account number, bank code, amount, reference)
  - RTGS batch template (ISO 20022 pacs.008 format)
  - EFT payroll template (employee ID, bank account, amount, KRA PIN)
  - Mixed rail template (rail type, identifier, amount, currency, purpose)
  - XML format template
  - JSON format template for API upload
- **Bulk approval workflows:**
  - First approver: Validate file integrity and totals
  - Second approver: Validate beneficiary list against sanctions
  - Final approver: Authorize execution
  - Approval delegation rules
- **Error report downloads:**
  - Failed rows with reason codes
  - Correction suggestions
  - Re-upload corrected file option
  - Partial execution report (which rows succeeded, which failed)

---








## Page 1.4 — Payment Rails & Routing

**Purpose:** Configuration and optimization of payment infrastructure with deep African rail support.

### Section 1.4.1 — Connected Banks Directory

- **Kenyan Banks:**
  - KCB Bank Kenya — API status, connection health, last sync, supported rails (PesaLink, RTGS, EFT, M-Pesa B2B), settlement windows, transaction limits, contact details
  - Equity Bank Kenya — Same details plus Equitel integration status
  - Co-operative Bank of Kenya — API status, Co-opNet integration, M-Pesa Paybill linkage
  - Stanbic Bank Kenya — API status, Blue247 integration, trade finance connectivity
  - ABSA Bank Kenya (formerly Barclays) — API status, supported rails
  - NCBA Bank — API status, Loop integration
  - Diamond Trust Bank (DTB) — API status
  - I&M Bank — API status
  - Standard Chartered Bank Kenya — API status
  - Family Bank — API status
  - SBM Bank — API status
  - All 40+ licensed Kenyan banks with connection status
- **East African Banks:**
  - Bank of Uganda connected banks
  - Bank of Tanzania connected banks
  - National Bank of Rwanda connected banks
  - Commercial Bank of Ethiopia (where permitted)
- **Major African Banks:**
  - Standard Bank (South Africa)
  - First Bank of Nigeria
  - Ecobank Transnational (pan-African)
  - Attijariwafa Bank (Morocco)
  - Banque Misr (Egypt)
  - Absa (South Africa, Botswana, Ghana, Uganda, Tanzania)
- **Global Correspondent Banks:**
  - JP Morgan Chase (USD clearing)
  - Citibank (multi-currency)
  - HSBC (GBP, EUR, Asia)
  - Deutsche Bank (EUR)
  - BNP Paribas (EUR, Africa)
  - Standard Chartered (Asia, Africa, Middle East)
- **Per-bank details:**
  - Connection status: Active, Degraded, Down, Maintenance
  - API health: Response time, error rate, uptime percentage
  - Last sync timestamp
  - Supported rails: PesaLink, RTGS, EFT, SWIFT, M-Pesa B2B, M-Pesa Paybill, M-Pesa Till, Mobile Money Interoperability
  - Settlement windows and cut-off times (EAT, CAT, WAT, GMT)
  - Bank-specific limits: Per transaction, daily, monthly
  - Special rules: Holiday schedules, weekend processing, same-day value cut-offs
  - API documentation link
  - Escalation contact for operations issues

### Section 1.4.2 — Mobile Money & PSP Directory

- **M-Pesa (Safaricom):**
  - Daraja API health and version
  - STK Push success rate and latency
  - B2C disbursement queue depth
  - C2B collection queue status
  - Paybill number management
  - Till number management
  - Settlement schedule: T+0 for most merchant tiers
  - Agent network liquidity status
  - Safaricom maintenance window calendar
  - API credential expiry tracking
- **Airtel Money:**
  - API health and connection status
  - Transaction success rate
  - Settlement timeline
  - Interoperability with M-Pesa status
  - Agent network status
- **T-Kash (Telkom Kenya):**
  - API health
  - Transaction volume
  - Interoperability status
- **MTN MoMo:**
  - Pan-African API status (17 markets)
  - Per-market connection health
  - Settlement arrangements
- **Orange Money:**
  - Francophone Africa API status
  - Connection health per market
- **PayPal:**
  - API health
  - Integration status (Kenya, Tanzania direct M-Pesa linkage)
  - Settlement timeline to local bank
  - Fee structure
- **Visa Direct / Mastercard Send:**
  - API health
  - Card push success rate
  - Settlement time
- **Equitel (Equity Bank):**
  - Thin SIM integration status
  - Transaction routing

### Section 1.4.3 — Routing Rules Engine

- **Smart routing configuration:**
  - **Rule 1 — Amount-based routing:**
    - KES < 1,000: M-Pesa STK Push (cheapest for micro)
    - KES 1,000 - 150,000: M-Pesa or PesaLink (speed vs. cost)
    - KES 150,000 - 999,999: PesaLink (instant, 24/7)
    - KES ≥ 1,000,000: RTGS (secure, high-value)
    - USD < 10,000: ACH or PayPal
    - USD ≥ 10,000: SWIFT gpi
  - **Rule 2 — Currency-based routing:**
    - KES domestic: PesaLink primary, RTGS for high value
    - KES↔UGX: EAPS or mobile money interoperability
    - KES↔TZS: EAPS or mobile money
    - KES↔USD: SWIFT or correspondent banking
    - EUR domestic: SEPA Instant
    - GBP domestic: FPS
  - **Rule 3 — Destination-based routing:**
    - To M-Pesa wallet: M-Pesa B2C or STK Push
    - To Airtel Money wallet: Airtel Money API or interoperability
    - To Kenyan bank: PesaLink (instant) or RTGS (high value)
    - To East African bank: EAPS
    - To African bank: PAPSS or SWIFT
    - To global bank: SWIFT gpi
    - To PayPal: PayPal API
  - **Rule 4 — Urgency-based routing:**
    - Critical (< 1 hour): M-Pesa, PesaLink, SEPA Instant, FPS
    - Urgent (< 4 hours): RTGS, SWIFT gpi, EAPS
    - Standard (< 24 hours): EFT, ACH, standard SWIFT
    - Non-urgent (> 24 hours): Cheapest available rail
  - **Rule 5 — Cost ceiling routing:**
    - Maximum acceptable fee percentage per transaction
    - Auto-fallback to cheaper rail if primary exceeds ceiling
  - **Rule 6 — Time-based routing:**
    - Banking hours: RTGS available
    - After hours: PesaLink, M-Pesa, SWIFT (if 24/7)
    - Weekends: Only 24/7 rails (PesaLink, M-Pesa, SEPA Instant)
    - Holidays: Kenyan public holiday calendar, East African holidays, global holidays
  - **Rule 7 — Customer segment routing:**
    - Premium customers: Fastest rail regardless of cost
    - Standard customers: Balanced speed-cost
    - Basic customers: Cheapest rail
  - **Rule 8 — Risk-based routing:**
    - High-risk transactions: Most reliable rail with full tracking
    - Low-risk transactions: Any available rail
- **Fallback rail configuration:**
  - Primary rail fails → try secondary → try tertiary
  - Auto-escalation if all rails fail
  - Fallback notification to operations team
- **A/B testing for routing optimization:**
  - Split traffic between two routing strategies
  - Measure: Success rate, cost, speed, customer satisfaction
  - Auto-adopt winning strategy after statistical significance

### Section 1.4.4 — Rail Performance Analytics

- **Success rate per rail over time:**
  - Daily, weekly, monthly trend charts
  - Target vs. actual comparison
  - Anomaly detection (sudden drops)
- **Average settlement time per rail:**
  - Mean, median, 95th percentile
  - Time-of-day patterns (slower during peak hours)
  - Day-of-week patterns
- **Cost per transaction per rail:**
  - Fixed fees, percentage fees, FX spreads
  - Total cost trend
  - Cost optimization suggestions
- **Failure reason analysis per rail:**
  - Top 10 failure reasons
  - Trending failure types
  - Resolution time per failure type
- **Rail capacity utilization:**
  - Transactions per second vs. maximum capacity
  - Queue depth during peak times
  - Capacity planning recommendations

### Section 1.4.5 — Rail Configuration

- **Enable/disable rails:**
  - Toggle per rail with reason and effective date
  - Impact assessment: How many pending transactions affected?
  - Auto-reroute pending transactions to alternative rail
- **Cut-off time management:**
  - Per-rail cut-off times with timezone display
  - Countdown timer to next cut-off
  - Cut-off override for emergency transactions (with approval)
- **Limit configuration:**
  - Per transaction minimum and maximum
  - Daily aggregate limit per rail
  - Monthly aggregate limit per rail
  - Per-customer limit per rail
  - Limit utilization dashboard
- **Credential and certificate management:**
  - API key rotation schedule
  - SSL certificate expiry tracking
  - OAuth token refresh automation
  - Daraja consumer key/secret management
  - PesaLink certificate management
  - SWIFT RMA authorization tracking
- **Webhook endpoint configuration per rail:**
  - Callback URL per event type
  - Webhook delivery status monitoring
  - Retry configuration
  - Webhook testing tool

### Section 1.4.6 — Nostro/Vostro Account Mapping

- **Account balances per rail/currency:**
  - KES float at Safaricom (M-Pesa business account)
  - KES nostro at KCB, Equity, Co-op, Stanbic
  - USD nostro at JP Morgan, Citi, StanChart
  - EUR nostro at Deutsche Bank, BNP Paribas
  - GBP nostro at HSBC, Barclays
  - UGX float at MTN Uganda, Airtel Uganda
  - TZS float at Vodacom Tanzania, Airtel Tanzania
  - Regional currency positions for EAPS
  - PAPSS pre-funding accounts
- **Reconciliation status per account:**
  - Last reconciliation date and time
  - Match rate percentage
  - Outstanding items count
  - Aging of unmatched items
- **Auto-sweep rules:**
  - Threshold-based sweeps (if balance > X, sweep to treasury)
  - Time-based sweeps (sweep at end of day)
  - Currency-based sweeps (consolidate all KES to primary account)
  - Minimum balance maintenance rules
- **FX position management:**
  - Net exposure per currency pair
  - Hedge ratio
  - Forward contract positions
  - Spot FX requirements

---

## Page 1.5 — Liquidity & Float Management

**Purpose:** Cash flow optimization across all nostro accounts, mobile money floats, and payment rails with African market specifics.

### Section 1.5.1 — Multi-Currency Liquidity Dashboard

- **Real-time balances across all accounts:**
  - **KES accounts:**
    - M-Pesa business float (Safaricom)
    - KCB nostro (current account, call account, fixed deposit)
    - Equity Bank nostro
    - Co-operative Bank nostro
    - Stanbic Bank nostro
    - ABSA Bank nostro
    - NCBA Bank nostro
  - **Regional currency accounts:**
    - UGX float (MTN Uganda, Airtel Uganda, Stanbic Uganda)
    - TZS float (Vodacom Tanzania, Airtel Tanzania, NMB Bank)
    - RWF float (MTN Rwanda, Airtel Rwanda, Bank of Kigali)
    - NGN float (GTBank Nigeria, First Bank, Zenith Bank)
    - GHS float (MTN Ghana, AirtelTigo, Ecobank Ghana)
    - ZAR float (Standard Bank, ABSA South Africa)
  - **Hard currency accounts:**
    - USD nostro at JP Morgan Chase (New York)
    - USD nostro at CitiBank (New York)
    - EUR nostro at Deutsche Bank (Frankfurt)
    - EUR nostro at BNP Paribas (Paris)
    - GBP nostro at HSBC (London)
    - GBP nostro at Barclays (London)
  - **PAPSS pre-funding accounts:**
    - Pre-funded clearing accounts per participating central bank
    - Utilization rate per account
    - Top-up requirements
- **Currency-wise position summary:**
  - Total assets per currency
  - Total obligations per currency (pending disbursements, committed facilities)
  - Net position per currency
  - Net position in base currency (KES) at current FX rates
- **Intraday liquidity forecast:**
  - Expected inflows next 1/4/8/24 hours per currency
  - Expected outflows next 1/4/8/24 hours per currency
  - Net position forecast with confidence intervals
  - Minimum balance alerts per account

### Section 1.5.2 — Cash Flow Forecasting

- **Predicted inflows/outflows (ML-powered):**
  - Historical pattern analysis per day of week, week of month, month of year
  - Seasonal trend identification (salary cycles, tax payment seasons, holiday spikes)
  - M-Pesa collection patterns (higher on weekends, month-end spikes)
  - PesaLink patterns (business hours concentration)
  - RTGS patterns (month-end, quarter-end spikes for corporate payments)
- **Scenario modeling:**
  - Best case: All scheduled inflows arrive on time, no unexpected outflows
  - Expected case: Historical average performance
  - Stress case: 20% of inflows delayed, 15% unexpected outflows
  - Black swan case: Major rail downtime, bank holiday extension, regulatory freeze
- **Cash flow gap alerts:**
  - Projected shortfall in any currency within next 24/48/72 hours
  - Auto-suggested funding actions
  - Early warning for KES liquidity (CBK reserve requirements)
- **Reconciliation with actuals:**
  - Forecast vs. actual comparison
  - Forecast accuracy tracking
  - Model retraining triggers

### Section 1.5.3 — Auto-Sweep & Rebalancing

- **Sweep rules configuration:**
  - **Threshold-based sweeps:**
    - If M-Pesa float > KES 50,000,000, sweep excess to KCB call account
    - If KCB current account > KES 100,000,000, sweep to fixed deposit
    - If USD nostro > USD 1,000,000, sweep to interest-bearing account
  - **Time-based sweeps:**
    - End-of-day sweep from all KES accounts to primary treasury account
    - Weekly sweep from regional currency accounts to USD (if surplus)
    - Monthly sweep from fixed deposits to operating accounts for planned outflows
  - **Currency-based sweeps:**
    - Consolidate all KES sub-accounts to primary KES account
    - Consolidate all USD accounts to primary USD account
  - **Rail-based sweeps:**
    - Sweep from PesaLink settlement account to primary account after cut-off
    - Sweep from M-Pesa settlement to primary account T+0 end of day
- **Inter-account transfer automation:**
  - Between PayMo's own accounts (no external rail needed)
  - Between partner bank accounts (using internal bank transfer)
  - Between mobile money floats (using provider APIs)
- **Minimum balance maintenance rules:**
  - Per account minimum balance with alert threshold
  - Auto-top-up from designated reserve account
  - Emergency funding trigger (call credit line)
- **Excess liquidity investment options:**
  


---

## Page 1.5 — Liquidity & Float Management (Continued)

### Section 1.5.3 — Auto-Sweep & Rebalancing (Continued)

- **Excess liquidity investment options:**
  - Central Bank of Kenya Treasury Bills (91-day, 182-day, 364-day) — auto-purchase when excess KES detected
  - Central Bank of Kenya Treasury Bonds — longer-term investment for structural surplus
  - Bank fixed deposits — negotiate rates with partner banks (KCB, Equity, Co-op)
  - Money market funds — Stanbic Money Market Fund, CIC Money Market Fund
  - Repurchase agreements (repos) — overnight and term repos with primary dealers
  - USD Treasury Bills — for USD surplus
  - Euro commercial paper — for EUR surplus
  - Regional central bank instruments — Bank of Uganda, Bank of Tanzania paper
  - Investment maturity ladder — ensure liquidity is available when needed
  - Yield comparison dashboard — compare returns across instruments
  - Risk rating per instrument (sovereign risk, counterparty risk, liquidity risk)

### Section 1.5.4 — Funding & Defunding

- **Request funding from partner bank:**
  - Credit line drawdown request form
  - Available credit lines per partner: KCB, Equity, Stanbic, ABSA, NCBA
  - Drawdown amount, currency, purpose
  - Interest rate terms (fixed, floating, KES benchmark + spread)
  - Tenor: overnight, 7 days, 30 days, 90 days, 1 year
  - Collateral requirements and available collateral
  - Approval workflow: Operations → Treasury → CFO
  - Drawdown confirmation and fund receipt tracking
- **Defund excess to treasury:**
  - Excess liquidity identification per account
  - Defund amount and destination (primary treasury, investment account)
  - Defund method: internal transfer, RTGS, SWIFT
  - Defund scheduling: immediate, end of day, end of week
  - Defund history and status
- **Funding history and status:**
  - All historical drawdowns with amount, date, tenor, rate, status
  - Outstanding drawdowns with maturity dates
  - Interest accrual tracking
  - Total cost of funding calculation
- **Interest accrual tracking:**
  - Daily interest accrual on credit lines
  - Interest payment schedule
  - Interest capitalization option
  - Effective annual rate calculation

### Section 1.5.5 — Liquidity Alerts & Limits

- **Low balance alerts per account:**
  - Threshold configuration per account per currency
  - Alert escalation: Warning (80% of threshold) → Critical (100%) → Emergency (120%)
  - Notification channels: In-app, SMS, email, Slack, PagerDuty
  - Alert suppression rules (e.g., suppress during known settlement windows)
- **Concentration risk alerts:**
  - Single bank concentration limit (max % of total liquidity at one bank)
  - Single currency concentration limit
  - Single rail concentration limit
  - Mobile money float concentration (max % at one MNO)
  - Alert when approaching limit, auto-action when exceeding
- **Regulatory liquidity ratio monitoring:**
  - CBK liquidity coverage ratio (LCR) — minimum 20% for Kenyan banks
  - Net stable funding ratio (NSFR) tracking
  - Cash reserve ratio (CRR) compliance
  - Local currency liquidity ratio
  - Foreign currency liquidity ratio
  - Daily reporting to CBK via KEPSS
- **Custom alert rule builder:**
  - Build custom alerts with drag-and-drop conditions
  - Conditions: account balance, currency, time, day, rail status, transaction volume
  - Actions: send notification, trigger sweep, block transactions, escalate to manager
  - Alert testing and simulation

### Section 1.5.6 — Mobile Money Float Management

- **M-Pesa float monitoring:**
  - Real-time float balance at Safaricom
  - Float utilization rate (used vs. available)
  - Float burn rate (how fast float depletes during peak hours)
  - Float top-up scheduling (auto-top-up when below threshold)
  - Float reconciliation: PayMo records vs. Safaricom statement
  - Float interest (if any) or cost of holding float
  - Agent network liquidity impact on float requirements
- **Cross-network float balancing:**
  - M-Pesa vs. Airtel Money vs. T-Kash float ratios
  - Customer preference analytics (which network do customers use most)
  - Auto-rebalancing between networks based on demand
  - Interoperability settlement reconciliation
- **Regional mobile money float:**
  - MTN MoMo float per country (Uganda, Tanzania, Rwanda, Ghana, Nigeria)
  - Airtel Money float per country
  - Orange Money float per country
  - Cross-border float transfer rules and costs

### Section 1.5.7 — FX Liquidity Management

- **FX position dashboard:**
  - Net open position per currency pair (KES/USD, KES/EUR, KES/GBP, KES/UGX, KES/TZS)
  - Position limits per pair (regulatory and internal)
  - Intraday position vs. overnight position
  - Position aging (how long has position been open)
- **FX hedging:**
  - Forward contract book: outstanding forwards, maturities, rates
  - FX option book: calls, puts, strikes, expiries
  - Natural hedging: matching inflows and outflows in same currency
  - Hedge effectiveness tracking
- **FX rate monitoring:**
  - Real-time rates from CBK, Reuters, Bloomberg
  - Rate alerts: significant movements, threshold breaches
  - Historical rate charts (1D, 1W, 1M, 1Y, 5Y)
  - Volatility indicators

---

## Page 1.6 — Reconciliation Center

**Purpose:** Automated and manual matching of transactions across all African and global rails, mobile money statements, and bank statements.

### Section 1.6.1 — Reconciliation Dashboard

- **Match rate percentage:**
  - Overall match rate across all rails
  - Per-rail match rate: M-Pesa, PesaLink, RTGS, EFT, SWIFT, EAPS, PAPSS, PayPal
  - Per-currency match rate
  - Trend over time (improving or deteriorating)
- **Unmatched items count:**
  - Total unmatched items
  - Per-rail unmatched count
  - Aging analysis: < 1 day, 1-3 days, 3-7 days, 7-30 days, > 30 days
  - Value of unmatched items
- **Breakdown by rail, currency, date range:**
  - Interactive charts and tables
  - Drill-down capability
- **Aging analysis of unmatched items:**
  - Heat map by age and value
  - Auto-escalation rules (escalate to manager after 3 days, to director after 7 days)
  - Write-off thresholds and approval workflow

### Section 1.6.2 — Auto-Reconciliation Engine

- **Matching rules configuration:**
  - **Exact match:** Amount, currency, reference, date all match exactly
  - **Fuzzy match:** Amount within tolerance (±0.01 or ±1%), date within ±1 day, reference partially matches
  - **Reference-based match:** Match on transaction reference number only
  - **Amount-date match:** Match on amount and date when reference is missing
  - **Multi-item match:** One bank statement line matches multiple internal transactions (batch)
  - **Split match:** One internal transaction matches multiple bank statement lines
- **Tolerance settings:**
  - Amount tolerance: absolute (e.g., ±KES 1) or percentage (e.g., ±0.5%)
  - Date tolerance: ±0 days (same day), ±1 day, ±3 days
  - Currency tolerance: exact match or converted at rate of day
- **Scheduled reconciliation jobs:**
  - M-Pesa: Every 15 minutes (high volume, real-time nature)
  - PesaLink: Every 30 minutes
  - RTGS: Every hour during banking hours
  - EFT: Daily at 6:00 AM (after overnight batch processing)
  - SWIFT: Every 2 hours
  - EAPS: Every hour
  - PAPSS: Every 2 hours
  - PayPal: Daily at 4:00 AM
  - Custom schedules per rail
- **Exception handling rules:**
  - Auto-match if confidence > 95%
  - Queue for manual review if confidence 70-95%
  - Flag for investigation if confidence < 70%
  - Auto-create adjustment entry for identified fee discrepancies

### Section 1.6.3 — Manual Reconciliation Workspace

- **Side-by-side comparison:**
  - Left panel: Internal transaction records (PayMo system)
  - Right panel: External statement (bank, MNO, PayPal)
  - Synchronized scrolling
  - Highlight differences in amount, date, reference, status
- **Suggested matches (AI-powered):**
  - Machine learning model suggests most likely matches
  - Confidence score per suggestion
  - One-click accept suggestion
  - Bulk accept suggestions above confidence threshold
- **Manual match actions:**
  - Match selected items
  - Split one item to match multiple
  - Combine multiple items to match one
  - Write off small differences (with approval and reason)
  - Create adjustment journal entry
  - Mark as "requires investigation" with assignee
- **Bulk reconciliation tools:**
  - Select all suggested matches and bulk accept
  - Bulk write-off for small differences under threshold
  - Bulk mark as "pending vendor response"

### Section 1.6.4 — Bank Statement Import

- **Multi-format support:**
  - **Kenyan bank formats:**
    - KCB: CSV, Excel, MT940
    - Equity: CSV, Excel, MT940, CAMT.053
    - Co-op: CSV, Excel
    - Stanbic: CSV, Excel, MT940, CAMT.053
    - ABSA: CSV, Excel, MT940
    - NCBA: CSV, Excel
    - Standard Chartered: MT940, CAMT.053
  - **Mobile money formats:**
    - Safaricom M-Pesa: CSV, Excel, API pull (Daraja)
    - Airtel Money: CSV, Excel
    - T-Kash: CSV, Excel
    - MTN MoMo: CSV, Excel, API pull
  - **Global formats:**
    - MT940 (SWIFT statement message)
    - CAMT.053 (ISO 20022 account report)
    - BAI2 (Bank Administration Institute format)
    - OFX (Open Financial Exchange)
    - CSV with configurable column mapping
    - Excel with multiple sheet support
    - ISO 20022 pain.002 (payment status report)
    - ISO 20022 pacs.002 (FIToFIPaymentStatusReport)
  - **API auto-import:**
    - Direct API connection to KCB, Equity, Stanbic, ABSA
    - Direct API to Safaricom Daraja for M-Pesa statements
    - Direct API to PayPal for transaction reports
    - SFTP auto-download from bank secure servers
    - Email auto-import (monitored inbox for statement attachments)
- **Statement parsing validation:**
  - Schema validation per format
  - Data type validation (dates, amounts, currencies)
  - Duplicate detection (prevent re-import of same statement)
  - Balance validation (opening + transactions = closing)
  - Error report with line-by-line detail
- **Import history and error logs:**
  - All imports with date, source, format, row count, success count, error count
  - Error log with reason and suggested fix
  - Re-import capability for failed files

### Section 1.6.5 — Reconciliation Reports

- **Daily reconciliation summary:**
  - Per-rail summary: total transactions, matched, unmatched, match rate
  - Aging of unmatched items
  - Action items for the day
  - Auto-generated at 6:00 AM
- **Outstanding items report:**
  - All unmatched items with detail
  - Assigned investigator
  - Days outstanding
  - Estimated resolution date
  - Escalation status
- **Adjustment journal entries:**
  - All adjustments made during reconciliation
  - Reason code, amount, account, approver
  - Linked to original transaction and statement
  - Audit trail
- **Audit-ready reconciliation certificates:**
  - Signed reconciliation certificate per period
  - CFO sign-off workflow
  - External auditor access (read-only)
  - Regulatory submission format (CBK, KRA, etc.)

---

## Page 1.7 — Settlement & Clearing

**Purpose:** End-of-day and real-time settlement operations across Kenyan, East African, African, and global clearing systems.

### Section 1.7.1 — Settlement Calendar

- **Daily settlement schedule per rail:**
  - **M-Pesa:** Real-time T+0 settlement, end-of-day net settlement to bank
  - **PesaLink:** Real-time 24/7, net settlement at 11:00 PM EAT
  - **RTGS (KEPSS):** Real-time during banking hours (8:00 AM - 3:00 PM EAT), final settlement at 3:00 PM
  - **EFT:** Batch settlement at 10:00 AM, 2:00 PM, 4:00 PM EAT
  - **SWIFT:** Value date based on message type and correspondent bank
  - **EAPS:** Daily settlement at 4:00 PM EAT across EAC central banks
  - **PAPSS:** Daily settlement at 3:00 PM GMT across African central banks
  - **SEPA Instant:** Real-time, net settlement at end of day
  - **ACH (US):** Settlement at 8:30 AM, 1:00 PM, 5:00 PM, 8:30 PM ET
  - **FPS (UK):** Real-time, net settlement at end of day
  - **PayPal:** Instant internal, bank withdrawal T+1 to T+3
- **Cut-off time countdown timers:**
  - Per-rail countdown to next cut-off
  - Visual urgency indicator (green > 2 hours, amber 30 min - 2 hours, red < 30 min)
  - Auto-alert at 30 minutes, 10 minutes, and 1 minute before cut-off
- **Holiday calendar per jurisdiction:**
  - Kenya: New Year's Day, Good Friday, Easter Monday, Labour Day, Madaraka Day, Eid al-Fitr (variable), Mashujaa Day, Jamhuri Day, Christmas Day, Boxing Day
  - Uganda: Independence Day, Martyrs' Day, etc.
  - Tanzania: Union Day, Saba Saba, Nyerere Day, etc.
  - Rwanda: Umuganura, Liberation Day, etc.
  - Nigeria: Democracy Day, Independence Day, etc.
  - Ghana: Independence Day, Republic Day, etc.
  - South Africa: Human Rights Day, Freedom Day, Youth Day, etc.
  - US: Federal holidays
  - UK: Bank holidays
  - EU: ECB holidays
  - Islamic holidays (variable dates): Eid al-Fitr, Eid al-Adha
- **Estimated settlement dates:**
  - Auto-calculation considering holidays, weekends, rail schedules
  - Display to customer at initiation
  - Update if conditions change (e.g., rail downtime)

### Section 1.7.2 — Netting & Batching

- **Gross vs. net settlement options:**
  - Gross settlement: Each transaction settled individually (RTGS, M-Pesa)
  - Net settlement: Offsetting transactions netted to single amount (EFT, PesaLink end-of-day)
  - Hybrid: Intraday net with end-of-day gross (some correspondent banking)
- **Batch creation and management:**
  - Auto-batch creation based on rules: rail, currency, value date, beneficiary bank
  - Manual batch creation for special handling
  - Batch content review and edit before submission
  - Batch submission status tracking
  - Batch rejection handling and resubmission
- **Multi-lateral netting calculations:**
  - Net position per participant in netting arrangement
  - Netting efficiency ratio (gross vs. net volume)
  - Netting agreement management
  - Dispute resolution for netting disagreements
- **Batch submission status:**
  - Submitted → Acknowledged → Validated → Accepted → Settled
  - Per-batch detail: count, value, participants, status
  - Batch-level rejection reasons and correction

### Section 1.7.3 — Settlement Reports

- **Pre-settlement validation reports:**
  - Liquidity sufficiency check per settlement account
  - Missing or incomplete transactions flagged
  - Limit breach warnings
  - Regulatory ratio impact preview
  - Auto-generated 1 hour before settlement
- **Post-settlement confirmation:**
  - Settlement completion confirmation per rail
  - Final positions per account
  - Discrepancy report (if any)
  - Settlement certificate generation
- **Settlement failure analysis:**
  - Failed settlement reasons: insufficient liquidity, system error, counterparty default, regulatory block
  - Impact assessment: which transactions affected, customer notification required
  - Resolution actions taken
  - Prevention measures for future
- **Central bank reporting (where applicable):**
  - CBK daily settlement report
  - CBK weekly liquidity report
  - CBK monthly payment system report
  - EAC cross-border settlement report
  - PAPSS settlement report

### Section 1.7.4 — End-of-Day (EOD) Process

- **EOD checklist and status:**
  - Pre-EOD tasks: All RTGS transactions submitted before 3:00 PM cut-off
  - EOD tasks: PesaLink net settlement, M-Pesa end-of-day reconciliation, EFT batch submission, SWIFT message queue processing
  - Post-EOD tasks: Statement downloads, reconciliation initiation, reporting generation
  - Per-task status: Pending, In Progress, Completed, Failed
  - Task owner and completion time
- **Automated EOD job monitoring:**
  - Real-time status of all automated EOD jobs
  - Job dependency chain visualization
  - Failed job auto-retry with escalation
  - EOD completion time tracking and SLA
- **EOD exception handling:**
  - Exception identification and categorization
  - Auto-assignment to on-call operations team
  - Escalation matrix: Operations → Manager → Director → CTO
  - Emergency EOD override procedures
- **Next-day opening position preview:**
  - Projected opening balances per account
  - Expected overnight inflows (e.g., M-Pesa T+0 settlement)
  - Scheduled outgoing payments for next business day
  - Liquidity adequacy forecast

---

## Page 1.8 — Transaction Analytics & Reporting

**Purpose:** Deep insights into transfer patterns, performance, and trends with African market focus.

### Section 1.8.1 — Volume & Value Analytics

- **Transaction count and value over time:**
  - Time series charts: hourly, daily, weekly, monthly, quarterly, yearly
  - Cumulative vs. periodic views
  - Year-over-year (YoY) comparison
  - Month-over-month (MoM) comparison
  - Week-over-week (WoW) comparison
- **Trend analysis:**
  - Linear trend line with R-squared
  - Seasonal decomposition (trend, seasonal, residual)
  - Growth rate tracking: absolute and percentage
  - Compound annual growth rate (CAGR)
- **Peak hour/day identification:**
  - Heat map by hour of day and day of week
  - Peak identification: highest volume hours, highest value hours
  - Off-peak identification for maintenance scheduling
  - Capacity planning based on peak projections
- **Growth rate tracking:**
  - Volume growth by product, rail, currency, corridor
  - Value growth by product, rail, currency, corridor
  - Customer growth correlation with transaction growth
  - Market share estimation vs. competitors

### Section 1.8.2 — Performance Metrics

- **Success rate trends:**
  - Overall success rate over time
  - Per-rail success rate: M-Pesa, PesaLink, RTGS, EFT, SWIFT, EAPS, PAPSS, PayPal
  - Per-currency success rate
  - Per-corridor success rate
  - Success rate by transaction value band
  - Success rate by time of day
- **Settlement time distribution:**
  - Histogram of actual settlement times per rail
  - Mean, median, mode, standard deviation
  - 50th, 75th, 90th, 95th, 99th percentile
  - SLA compliance rate (percentage within promised time)
  - Settlement time by beneficiary bank
- **Failure reason breakdown:**
  - Top 20 failure reasons across all rails
  - Per-rail failure reason distribution
  - Trending failure types (increasing or decreasing)
  - Failure reason correlation with time, amount, currency, corridor
  - Resolution time per failure type
- **Retry success rates:**
  - First attempt success rate
  - Second attempt success rate
  - Third+ attempt success rate
  - Optimal retry strategy per failure type
  - Cost of retries vs. value of successful completion

### Section 1.8.3 — Revenue & Cost Analysis

- **Fee revenue per rail, per client, per corridor:**
  - M-Pesa revenue: STK Push fees, B2C fees, C2B merchant discount rate
  - PesaLink revenue: per-transaction fees, monthly subscription fees
  - RTGS revenue: high-value transaction fees
  - EFT revenue: batch processing fees
  - SWIFT revenue: message fees, correspondent bank fees markup
  - FX spread revenue: difference between interbank rate and customer rate
  - Corridor-specific revenue: KES→UGX, KES→TZS, KES→USD, etc.
- **Cost per transaction breakdown:**
  - Rail cost: what PayMo pays to MNO, bank, or network
  - Infrastructure cost: servers, bandwidth, API calls
  - Operations cost: manual handling, reconciliation, support
  - Compliance cost: screening, reporting, audit
  - Total cost per transaction per rail
  - Cost trend over time (negotiating better rates, volume discounts)
- **Margin analysis:**
  - Gross margin per transaction (revenue - rail cost)
  - Net margin per transaction (revenue - total cost)
  - Margin by product, rail, currency, corridor, customer segment
  - Margin trend and optimization opportunities
- **Profitability by payment corridor:**
  - KES domestic: M-Pesa, PesaLink, RTGS, EFT
  - KES↔UGX: EAPS, mobile money interoperability
  - KES↔TZS: EAPS, mobile money interoperability
  - KES↔USD: SWIFT, correspondent banking
  - KES↔EUR: SWIFT, SEPA
  - KES↔GBP: SWIFT, FPS
  - USD domestic: ACH, Wire
  - EUR domestic: SEPA, SEPA Instant
  - GBP domestic: FPS
  - PayPal global corridor

### Section 1.8.4 — Custom Report Builder

- **Drag-and-drop report designer:**
  - Data source selection: transactions, settlements, reconciliations, liquidity, compliance
  - Field selection and ordering
  - Filter configuration
  - Grouping and aggregation options
  - Sorting configuration
  - Chart type selection: table, bar, line, pie, heatmap, map, funnel
- **Pre-built templates:**
  - Daily Operations Report: All transactions, success rates, exceptions, liquidity position
  - Monthly Board Report: Strategic KPIs, growth, profitability, risk metrics
  - Regulatory Report: CBK required format, transaction volumes, values, rail breakdown
  - Client Statement: Per-client transaction summary, fees, balances
  - M-Pesa Performance Report: STK Push success, B2C queue, float position
  - PesaLink Performance Report: Interbank volume, bank connectivity, uptime
  - Cross-Border Report: EAPS, PAPSS, SWIFT volumes and values
  - FX Report: Currency flows, hedge positions, P&L
  - Compliance Report: Screening hits, SARs filed, regulatory submissions
  - Audit Report: All user actions, data changes, system events
- **Scheduled report generation and delivery:**
  - Schedule: hourly, daily, weekly, monthly, quarterly, annually
  - Delivery method: email, SFTP, API webhook, in-app notification
  - Format: PDF, Excel, CSV, JSON, XML
  - Recipient management: internal users, external regulators, clients
  - Delivery confirmation tracking
- **Export formats:**
  - PDF: Formatted with logo, headers, footers, page numbers
  - Excel: Multiple sheets, formulas, pivot tables, charts
  - CSV: Raw data for import into other systems
  - JSON: Machine-readable for API integration
  - XML: ISO 20022 format for regulatory submission

### Section 1.8.5 — Real-Time Monitoring

- **Live transaction heatmap:**
  - Geographic heatmap: transaction origin and destination by country, region, city
  - Time-based heatmap: transactions by hour and day
  - Rail-based heatmap: transactions by rail and status
  - Value-based heatmap: high-value transaction concentration
  - Interactive drill-down: click region to see detail
- **Geographic flow visualization:**
  - Sankey diagram showing money flows between countries, banks, rails
  - Flow thickness proportional to value
  - Direction arrows showing inflow vs. outflow
  - Net flow per corridor
  - Animation showing flow over time
- **Anomaly detection alerts:**
  - Statistical anomaly: volume/value deviation > 3 standard deviations from mean
  - Behavioral anomaly: unusual pattern (e.g., sudden spike in M-Pesa reversals)
  - Fraud pattern anomaly: structuring, rapid-fire transactions, round amounts
  - System anomaly: sudden drop in success rate for a rail
  - Alert generation with severity, suggested action, auto-suppression rules
- **SLA compliance tracking:**
  - Per-SLA metric: settlement time, success rate, availability, support response time
  - SLA dashboard: green (compliant), amber (at risk), red (breached)
  - SLA breach root cause analysis
  - SLA credit calculation (refunds for breaches)
  - SLA improvement trend

---

## Page 1.9 — Compliance & AML (Transactions)

**Purpose:** Transaction-level compliance monitoring and regulatory reporting with Kenya-specific requirements.

### Section 1.9.1 — Transaction Screening

- **Real-time sanctions screening:**
  - Lists: OFAC (US), UN Security Council, EU Consolidated List, UK Sanctions List, HMT (UK Treasury)
  - Local lists: CBK sanctions list, Kenyan government prohibited persons, EAC sanctions
  - Screening against: sender name, receiver name, beneficiary name, bank name, MNO name, reference text, narrative
  - Fuzzy matching with confidence score
  - False positive management: whitelist, previous disposition, auto-clear rules
  - Screening hit review and disposition workflow:
    - Hit identified → Alert generated → Analyst review → Disposition (clear / confirm match / escalate)
    - Disposition options: False positive, True positive (block and report), Requires further investigation
    - Audit trail of all dispositions
    - SLA: Review within 4 hours of hit
- **PEP (Politically Exposed Persons) screening:**
  - Global PEP databases: Dow Jones, Refinitiv World-Check, LexisNexis
  - Local PEP lists: Kenyan MPs, Cabinet Secretaries, Governors, MCAs, EAC officials, African Union officials
  - Family members and close associates screening
  - PEP risk rating: High (head of state), Medium (MP, governor), Low (MCA)
  - Enhanced due diligence triggers for PEP transactions
  - Ongoing monitoring: PEP status changes, new appointments, removals
- **Adverse media monitoring:**
  - News feed scanning for negative mentions of transaction parties
  - Sources: local Kenyan media (Daily Nation, The Standard, Business Daily), African media, international media
  - Keywords: fraud, corruption, money laundering, terrorism, sanctions, investigation
  - Alert generation for adverse media hits
  - Manual review and disposition workflow
- **Screening hit review and disposition:**
  - Queue of all pending screening hits
  - Per-hit detail: matched name, matched list, confidence score, transaction detail
  - Analyst assignment and workload balancing
  - Disposition tracking and reporting
  - Quality assurance: random sample review by senior analyst

### Section 1.9.2 — AML Monitoring

- **Suspicious transaction detection rules:**
  - **Structuring/smurfing detection:** Multiple transactions just below reporting threshold (e.g., KES 999,000 when threshold is KES 1,000,000)
  - **Rapid movement detection:** Funds received and immediately transferred out (velocity)
  - **Round amount detection:** Unusual frequency of round amounts (e.g., KES 100,000, KES 500,000)
  - **Off-hours activity:** Transactions outside normal business hours for the customer profile
  - **Geographic risk:** Transactions to/from high-risk jurisdictions (FATF grey list, black list)
  - **Counterparty risk:** Transactions with known high-risk entities
  - **Behavioral deviation:** Transaction pattern significantly different from customer's historical behavior
  - **M-Pesa specific:** Multiple STK Push requests to same number, unusually high C2B collections
  - **Cross-border specific:** Sudden increase in remittances, structuring across corridors
- **Threshold monitoring:**
  - CBK reporting threshold: KES 1,000,000 (approximately USD 7,500) for CTR
  - EAC cross-border reporting thresholds
  - FATF Recommendation 16 threshold for wire transfers
  - Custom thresholds per customer risk profile
  - Threshold breach alerts and auto-reporting
- **Transaction pattern analysis:**
  - Customer transaction profile: expected volume, value, frequency, counterparties, rails
  - Deviation scoring: how much does current behavior deviate from profile
  - Peer group comparison: how does customer compare to similar customers
  - Network analysis: identify clusters of related accounts
  - Graph visualization of transaction networks

### Section 1.9.3 — Regulatory Reporting

- **CTR (Currency Transaction Report) generation:**
  - CBK Form CTR-001 for cash transactions > KES 1,000,000
  - Auto-generation when threshold breached
  - Customer detail: name, ID, address, occupation, source of funds
  - Transaction detail: amount, currency, date, purpose, counterparty
  - Filing to Financial Reporting Centre (FRC) of Kenya
  - Filing status tracking and confirmation
- **SAR (Suspicious Activity Report) filing:**
  - SAR Form for suspicious transactions regardless of amount
  - Narrative generation: auto-draft based on alert triggers
  - Supporting evidence attachment: transaction records, screening hits, adverse media
  - Filing to FRC within 24 hours of identification
  - Filing status tracking
  - Follow-up with FRC: requests for additional information, feedback
- **Cross-border reporting:**
  - CBK cross-border transaction reporting
  - EAC cross-border payment reporting
  - FATF wire transfer information requirements (originator and beneficiary information)
  - SWIFT MT202COV compliance for cover payments
- **Regulatory filing status tracking:**
  - Calendar of all upcoming filing deadlines
  - Filing completion status per report
  - Overdue filing alerts with escalation
  - Historical filing archive
  - Regulatory feedback and correspondence management
- **Report history and audit trail:**
  - All filed reports with date, content, filer, status
  - Amendment tracking if report corrected
  - Regulatory response tracking
  - Audit trail for examiner review

### Section 1.9.4 — Audit Trail

- **Immutable transaction logs:**
  - Every transaction logged with: ID, timestamp, amount, currency, sender, receiver, rail, status, user, IP, device
  - Cryptographic hash for tamper detection
  - Blockchain-style chaining for integrity
  - Retention: 7 years minimum (per CBK requirements)
- **User action logging:**
  - Every user action logged: login, logout, view, create, edit, approve, reject, export
  - Action detail: what changed, from what to what
  - User identity, role, department
  - IP address, geolocation, device fingerprint
  - Session ID and duration
- **Data change tracking:**
  - Field-level change tracking for all master data
  - Before and after values
  - Change reason (mandatory for sensitive fields)
  - Approval workflow for sensitive changes
- **Compliance evidence repository:**
  - All compliance-related documents: KYC files, screening results, SARs, CTRs, audit reports
  - Document versioning
  - Access control: who can view, edit, delete
  - Retention policy enforcement
  - Legal hold capability (prevent deletion for litigation)

---

## Page 1.10 — API & Integration Management

**Purpose:** Developer portal for bank, MNO, PSP, and client integrations with African market focus.

### Section 1.10.1 — API Keys & Credentials

- **Key generation and rotation:**
  - Generate API keys for: banks, MNOs, PSPs, corporate clients, fintech partners, government agencies
  - Key types: Production, Sandbox, Read-only, Webhook
  - Auto-rotation schedule: 90 days, 180 days, 365 days
  - Rotation notification: 30 days, 7 days, 1 day before expiry
  - Emergency rotation capability
  - Key revocation with immediate effect
- **Scope and permission management:**
  - Granular permissions per API endpoint
  - Resource-level access control (account, transaction, customer)
  - Action-level access control (create, read, update, delete, approve)
  - Role-based permission templates: Bank Integration, MNO Integration, Corporate Client, Fintech Partner, Government, Auditor
  - Custom permission builder
- **IP whitelisting:**
  - Per-API-key allowed IP ranges
  - Geo-blocking: allow only from specific countries
  - VPN detection and handling
  - IP change notification and approval workflow
- **Usage quotas and throttling:**
  - Rate limits: requests per second, per minute, per hour, per day
  - Burst allowance configuration
  - Quota utilization dashboard
  - Throttling behavior: queue, reject, or degrade
  - Quota increase request workflow

### Section 1.10.2 — Webhook Management

- **Webhook endpoint configuration:**
  - Per-integration webhook URL
  - Supported events: transaction.created, transaction.completed, transaction.failed, transaction.reversed, settlement.completed, reconciliation.matched, compliance.alert, liquidity.low, rate.changed
  - Event filtering: subscribe to specific events only
  - Payload format: JSON, XML, form-encoded
  - Custom headers for authentication
- **Webhook delivery status and retry logs:**
  - Real-time delivery status: Delivered, Failed, Retrying, Queued
  - Delivery latency tracking
  - Retry schedule: immediate, 5 min, 15 min, 1 hour, 4 hours, next day
  - Max retry count: configurable per integration
  - Dead letter queue for permanently failed webhooks
  - Manual retry capability
- **Webhook testing tool:**
  - Send test webhook to endpoint
  - Verify signature validation
  - Inspect payload structure
  - Test retry behavior
  - Load test with simulated high volume

### Section 1.10.3 — API Documentation

- **Interactive API explorer (Swagger/OpenAPI):**
  - All endpoints documented with request/response schemas
  - Try-it-now functionality with sandbox environment
  - Authentication examples
  - Error code reference
  - Rate limit headers explanation
- **Code samples in multiple languages:**
  - JavaScript/Node.js
  - Python
  - Java
  - C#
  - PHP
  - Ruby
  - Go
  - cURL examples
  - Postman collection download
- **SDK downloads:**
  - PayMo JavaScript SDK
  - PayMo Python SDK
  - PayMo Java SDK
  - PayMo Android SDK (for mobile integrations)
  - PayMo iOS SDK
  - M-Pesa Daraja wrapper SDK
  - PesaLink integration SDK
- **Changelog and versioning:**
  - API version history
  - Breaking change notifications
  - Deprecation schedule
  - Migration guides between versions
  - Sunset dates for deprecated versions

### Section 1.10.4 — Integration Health

- **Connected client systems status:**
  - Per-integration health dashboard
  - Connection status: Healthy, Degraded, Down, Maintenance
  - Last successful API call timestamp
  - Last failed API call timestamp and reason
- **API call volume and latency:**
  - Requests per minute/hour/day per integration
  - Average response time per endpoint
  - 95th percentile response time
  - Error rate per integration
  - Trend analysis: improving or deteriorating
- **Error rate monitoring:**
  - Top error codes per integration
  - Error trend over time
  - Error correlation with system changes
  - Auto-alert when error rate exceeds threshold
- **Integration performance scorecards:**
  - Score per integration: availability, latency, error rate, usage
  - Grade: A (excellent), B (good), C (fair), D (poor), F (critical)
  - Performance improvement recommendations
  - Quarterly integration review scheduling

### Section 1.10.5 — Sandbox Environment

- **Test account management:**
  - Create test accounts for: KES, USD, EUR, UGX, TZS
  - Test M-Pesa wallet simulation
  - Test bank account simulation (KCB, Equity, Co-op, Stanbic)
  - Test PayPal account simulation
  - Reset test data capability
- **Mock transaction generation:**
  - Generate mock M-Pesa STK Push transactions
  - Generate mock PesaLink transfers
  - Generate mock RTGS transactions
  - Generate mock SWIFT transfers
  - Generate mock EAPS cross-border transactions
  - Generate mock compliance alerts
  - Bulk mock data generation for load testing
- **Scenario simulation:**
  - Successful transaction flow
  - Failed transaction flow (insufficient funds, invalid account, timeout)
  - Reversed transaction flow
  - Compliance hold flow
  - Multi-currency FX flow
  - Cross-border EAPS flow
  - Bulk disbursement flow
  - Webhook delivery flow
- **Sandbox-to-production migration tools:**
  - Configuration comparison: sandbox vs. production
  - Migration checklist
  - Gradual traffic shifting (10%, 25%, 50%, 100%)
  - Rollback capability
  - Production verification tests

---

## Page 1.11 — Mobile Money & PSP Integration Hub

**Purpose:** Dedicated management center for mobile money operators, PSPs, and alternative payment methods — the backbone of African payments.

### Section 1.11.1 — M-Pesa Integration Management

- **Daraja API Configuration:**
  - Consumer key and secret management
  - API version tracking (Daraja v1, v2, v3)
  - Environment toggle: Sandbox, Production
  - API endpoint configuration: STK Push, B2C, C2B, Account Balance, Transaction Status, Reversal
  - OAuth token management: generation, refresh, expiry monitoring
  - Passkey management for STK Push
  - Shortcode configuration: Paybill numbers, Till numbers, B2C organization shortcode
  - Initiator name and security credential management
- **STK Push Management:**
  - Real-time queue depth and processing rate
  - Success rate by hour, by amount band, by customer segment
  - Timeout analysis: average time to customer PIN entry
  - Cancellation rate and reasons
  - Retry strategy for failed STK Push
  - Customer notification customization
- **B2C Disbursement Management:**
  - Queue management: pending, processing, completed, failed
  - Disbursement scheduling: immediate, batch, recurring
  - Per-transaction and daily limits monitoring
  - Failed disbursement retry logic
  - Disbursement to unregistered M-Pesa users handling
  - Disbursement confirmation callback processing
- **C2B Collection Management:**
  - Paybill number performance: volume, value, success rate
  - Till number performance
  - Callback URL configuration and health
  - Validation and confirmation URL management
  - Duplicate transaction handling
  - Settlement reconciliation: M-Pesa records vs. PayMo records
- **M-Pesa Statement Integration:**
  - Auto-pull M-Pesa statement via Daraja API
  - Statement parsing and reconciliation
  - Discrepancy identification and resolution
  - Historical statement archive

### Section 1.11.2 — Airtel Money Integration

- **API Configuration:**
  - Airtel Money API credentials
  - Endpoint configuration
  - OAuth token management
- **Transaction Management:**
  - Collection (C2B) configuration
  - Disbursement (B2C) configuration
  - Transaction status inquiry
  - Reversal handling
- **Interoperability Status:**
  - M-Pesa ↔ Airtel Money rail health
  - Transaction success rate cross-network
  - Settlement reconciliation

### Section 1.11.3 — T-Kash Integration

- **API Configuration:**
  - Telkom T-Kash API credentials
  - Endpoint and token management
- **Transaction Management:**
  - Collection and disbursement
  - Status inquiry
  - Reconciliation

### Section 1.11.4 — MTN MoMo Integration

- **Pan-African API Configuration:**
  - MTN MoMo API credentials per country: Uganda, Tanzania, Rwanda, Ghana, Nigeria, Ivory Coast, Cameroon, Congo, Swaziland, Zambia, Benin, Guinea, Liberia, South Sudan
  - Sandbox and production environment per country
  - API key rotation per country
- **Per-Country Transaction Management:**
  - Collection (request-to-pay) configuration
  - Disbursement (transfer) configuration
  - Balance inquiry
  - Transaction status inquiry
  - User info inquiry (KYC validation)
  - Account holder validation
- **Cross-Border MoMo:**
  - MTN MoMo cross-border transfer configuration
  - Corridor-specific settings
  - FX handling for cross-border

### Section 1.11.5 — PayPal Integration

- **API Configuration:**
  - PayPal REST API credentials (Client ID, Secret)
  - Environment: Sandbox, Production
  - Webhook ID configuration
  - API version tracking
- **Transaction Management:**
  - PayPal to PayMo deposit processing
  - PayMo to PayPal withdrawal processing
  - PayPal Express Checkout integration
  - PayPal Payouts (mass payment) for bulk disbursements
  - Transaction fee tracking and reconciliation
- **M-Pesa ↔ PayPal Linkage:**
  - Kenya-specific M-Pesa to PayPal top-up
  - PayPal to M-Pesa withdrawal
  - Transaction limit management
  - FX rate display and lock

### Section 1.11.6 — Card Integration (Visa Direct / Mastercard Send)

- **API Configuration:**
  - Visa Direct API credentials
  - Mastercard Send API credentials
  - Certificate management
- **Push-to-Card Functionality:**
  - Card eligibility check (BIN range validation)
  - Push payment initiation
  - Transaction status tracking
  - Reversal handling
- **Dispute Management:**
  - Chargeback handling
  - Dispute evidence submission
  - Win/loss tracking

### Section 1.11.7 — Equitel (Equity Bank) Integration

- **Thin SIM Integration:**
  - Equitel API configuration
  - Transaction routing via Equitel
  - Balance inquiry
  - Statement integration

---

## Page 1.12 — KRA & Government Integration

**Purpose:** Integration with Kenya Revenue Authority and government payment systems for tax compliance and G2P/P2G transactions.

### Section 1.12.1 — KRA eTIMS Integration

- **eTIMS API Configuration:**
  - KRA eTIMS API credentials
  - Environment: Sandbox, Production
  - Token management and refresh
- **Tax Invoice Processing:**
  - Real-time tax invoice validation
  - Invoice number verification
  - Tax amount validation
  - KRA PIN validation
  - Invoice status: Valid, Invalid, Cancelled, Expired
- **Transaction Hold for Tax Verification:**
  - Auto-hold transactions pending eTIMS validation
  - Release upon validation success
  - Reject upon validation failure
  - Manual override with approval

### Section 1.12.2 — iTax Integration

- **iTax API Configuration:**
  - KRA iTax API credentials
  - Taxpayer PIN validation
- **Tax Payment Processing:**
  - Income tax payment
  - VAT payment
  - PAYE payment
  - Withholding tax payment
  - Stamp duty payment
  - Excise duty payment
  - Customs duty payment
- **Tax Payment Status Tracking:**
  - Payment acknowledgment from KRA
  - Receipt generation
  - Tax compliance certificate check

### Section 1.12.3 — GavaConnect Integration

- **Government Payment Portal:**
  - Integration with GavaConnect for government service payments
  - Passport application fees
  - Driving license fees
  - Business registration fees
  - Land rates
  - Court fees
  - Police abstract fees
  - NHIF payments
  - NSSF payments

### Section 1.12.4 — E-Citizen Integration

- **E-Citizen Platform:**
  - Integration with Kenya e-Citizen portal
  - Government service payment routing
  - Single sign-on capability
  - Payment confirmation to e-Citizen

---

## Page 1.13 — Multi-Currency & FX Management

**Purpose:** Comprehensive foreign exchange operations supporting African and global currencies.

### Section 1.13.1 — Live FX Rates Board

- **Real-time mid-market rates:**
  - KES/USD, KES/EUR, KES/GBP, KES/CHF, KES/JPY, KES/CNY
  - KES/UGX, KES/TZS, KES/RWF, KES/SSP
  - USD/EUR, USD/GBP, EUR/GBP
  - NGN/USD, GHS/USD, ZAR/USD
  - Source: CBK daily rate, Reuters, Bloomberg, central bank rates
- **Bid/ask spreads:**
  - PayMo customer buy rate (bid)
  - PayMo customer sell rate (ask)
  - Spread percentage and absolute value
  - Spread comparison to competitors
- **Rate history charts:**
  - Intraday (1-minute intervals)
  - Daily (last 30 days)
  - Weekly (last 52 weeks)
  - Monthly (last 5 years)
  - Annotations for significant events (CBK rate decisions, elections, global events)
- **Rate alert configuration:**
  - Target rate alert: notify when rate reaches desired level
  - Threshold alert: notify when rate moves beyond threshold
  - Volatility alert: notify when rate volatility exceeds threshold
  - Delivery: in-app, SMS, email, webhook

### Section 1.13.2 — FX Conversion

- **Spot conversion tool:**
  - Amount and currency pair selection
  - Direction: buy foreign currency, sell foreign currency
  - Real-time rate display with 15-minute lock
  - Rate countdown timer
  - Settlement date selection (T+0, T+1, T+2)
- **Fee and spread disclosure:**
  - Interbank rate
  - PayMo spread applied
  - Customer rate
  - Total cost in base currency
  - Effective cost percentage
- **Transaction limit checks:**
  - Per-transaction limit
  - Daily limit
  - Customer segment limit
  - Regulatory limit (if any)

### Section 1.13.3 — Forward Contracts & Hedging

- **Forward contract creation:**
  - Currency pair, amount, tenor (1W to 12M)
  - Forward rate calculation (spot + forward points)
  - Forward points display
  - Settlement date
- **Hedge ratio configuration:**
  - Percentage of exposure to hedge
  - Natural hedge offset
  - Net hedge position
- **Mark-to-market valuation:**
  - Daily revaluation of outstanding forwards
  - Unrealized P&L
  - Collateral requirement calculation
- **Hedge effectiveness reporting:**
  - Hedge ratio achievement
  - Basis risk tracking
  - Ineffectiveness measurement

### Section 1.13.4 — Multi-Currency Wallets

- **Wallet balances per currency:**
  - KES wallet
  - USD wallet
  - EUR wallet
  - GBP wallet
  - UGX wallet
  - TZS wallet
  - And all supported currencies
- **Currency conversion history:**
  - All conversions with date, amount, rate, cost
  - Cumulative conversion volume per currency pair
  - Average achieved rate vs. market rate
- **Wallet-to-wallet transfers:**
  - Instant transfer between own wallets
  - FX applied at current rate
  - No fee for internal transfers
- **Currency exposure summary:**
  - Net long/short per currency
  - Exposure as percentage of total assets
  - Concentration risk alerts

### Section 1.13.5 — Treasury Analytics

- **Currency exposure heatmap:**
  - Visual heatmap of net positions
  - Green (hedged), yellow (partially hedged), red (unhedged)
  - Drill-down per currency pair
- **VaR (Value at Risk) calculations:**
  - 1-day VaR at 95% and 99% confidence
  - 10-day VaR for regulatory reporting
  - Historical simulation method
  - Parametric method
  - Monte Carlo simulation
- **Hedge ratio tracking:**
  - Target hedge ratio vs. actual
  - Trend over time
  - Rebalancing recommendations
- **P&L from FX operations:**
  - Realized P&L from settled trades
  - Unrealized P&L from open positions
  - Total FX P&L
  - P&L attribution: trading, translation, transaction

---

## Page 1.14 — Customer & Account Management

**Purpose:** Management of PayMo customer accounts, KYC/KYB, and relationship data.

### Section 1.14.1 — Customer Directory

- **Retail customers:**
  - Individual profiles: name, ID number (Kenyan national ID, passport), date of birth, address, phone, email
  - KYC status: Pending, In Progress, Verified, Enhanced, Restricted
  - Risk rating: Low, Medium, High
  - Account types: Wallet, Bank-linked, Card-linked
  - Transaction history summary
- **SME customers:**
  - Business profiles: company name, registration number, KRA PIN, business type, industry
  - KYB status and documents
  - Directors and beneficial owners
  - Business bank accounts linked
  - Credit facilities active
- **Corporate customers:**
  - Company profiles: legal name, registration, tax ID, industry, turnover
  - Treasury contacts
  - Authorized signatories
  - Credit limits and utilization
  - Integration APIs active
- **Real estate developers:**
  - Developer profiles: company, projects, licenses
  - Project-specific accounts
  - Construction finance facilities

### Section 1.14.2 — KYC/KYB Management

- **Document collection and verification:**
  - ID verification: Kenyan national ID (Huduma Namba), passport, driving license, alien ID
  - Address verification: utility bill, bank statement, tenancy agreement
  - Business registration: certificate of incorporation, CR12, memorandum
  - Tax compliance: KRA PIN, tax compliance certificate
  - Beneficial ownership declaration
  - PEP declaration
- **Verification status tracking:**
  - Per-document status: Uploaded, Under Review, Verified, Rejected, Expired
  - Overall KYC status
  - Expiry alerts (ID expiry, business license expiry)
- **Enhanced due diligence:**
  - Trigger conditions: high-risk country, high-risk business, PEP, adverse media
  - EDD document requirements
  - EDD approval workflow
  - Ongoing monitoring triggers

### Section 1.14.3 — Account Configuration

- **Account types:**
  - Personal wallet (KES, multi-currency)
  - Business current account
  - Business savings account
  - Escrow account
  - Collection account (Paybill/Till linked)
  - Disbursement account (B2C linked)
- **Account limits:**
  - Transaction limits per type
  - Daily, weekly, monthly limits
  - Limit increase request workflow
- **Account status management:**
  - Active, Dormant, Frozen, Suspended, Closed
  - Status change reason and approval
  - Customer notification

---

## Page 1.15 — Fee & Commission Management

**Purpose:** Configuration and management of all fees, commissions, and pricing across the platform.

### Section 1.15.1 — Fee Structure Configuration

- **Transaction fees per rail:**
  - M-Pesa STK Push: percentage or flat fee
  - M-Pesa B2C: tiered fee structure
  - M-Pesa C2B: merchant discount rate
  - PesaLink: flat fee per transaction
  - RTGS: flat fee based on amount band
  - EFT: flat fee or per-item fee
  - SWIFT: message fee + correspondent fee markup
  - SEPA: flat fee
  - ACH: flat fee
  - PayPal: percentage markup
- **FX fees:**
  - Spread per currency pair
  - Minimum spread
  - Volume-based spread tiers
- **Account fees:**
  - Monthly maintenance fee
  - Minimum balance fee
  - Dormancy fee
  - Statement fee
- **Service fees:**
  - KYC verification fee
  - API access fee
  - Premium support fee
  - Chargeback fee
  - Reversal fee

### Section 1.15.2 — Commission Management

- **Agent commissions:**
  - Cash-in commission
  - Cash-out commission
  - Bill payment commission
  - Airtime purchase commission
- **Partner commissions:**
  - Merchant commission for C2B
  - Bank partner commission
  - MNO partner commission
  - Referral commission
- **Commission calculation and settlement:**
  - Real-time commission accrual
  - Commission statement generation
  - Commission payment scheduling
  - Commission reconciliation

### Section 1.15.3 — Promotional Pricing

- **Campaign management:**
  - Campaign creation: name, duration, target segment, products
  - Discount types: percentage off, flat discount, waived fee
  - Eligibility rules
  - Usage limits per customer
- **Campaign performance:**
  - Uptake rate
  - Revenue impact
  - Customer acquisition cost
  - ROI calculation

---

## Page 1.16 — Dispute & Chargeback Management

**Purpose:** Management of customer disputes, chargebacks, and transaction reversals.

### Section 1.16.1 — Dispute Intake

- **Dispute channels:**
  - Customer self-service portal
  - Customer support hotline
  - Email
  - In-app chat
  - Social media monitoring
- **Dispute categorization:**
  - Unauthorized transaction
  - Incorrect amount
  - Duplicate transaction
  - Non-receipt of goods/services
  - Goods not as described
  - Refund not processed
  - M-Pesa STK Push not received
  - Wrong beneficiary credited
- **Dispute form:**
  - Transaction reference
  - Dispute reason
  - Evidence upload
  - Expected resolution

### Section 1.16.2 — Dispute Investigation

- **Investigation workflow:**
  - Auto-assignment to investigator
  - Transaction trace and audit
  - Beneficiary bank/MNO inquiry
  - Evidence collection
  - Customer communication
- **SLA tracking:**
  - Acknowledgment: 24 hours
  - Investigation: 5 business days
  - Resolution: 10 business days
  - Escalation triggers

### Section 1.16.3 — Resolution & Compensation

- **Resolution options:**
  - Uphold (transaction valid)
  - Reverse (refund customer)
  - Partial refund
  - Goodwill gesture
  - Escalate to arbitration
- **Compensation processing:**
  - Refund initiation
  - Compensation calculation (principal + interest + fees)
  - Customer notification
  - General ledger posting

### Section 1.16.4 — Chargeback Management

- **Chargeback intake:**
  - Card scheme chargeback (Visa, Mastercard)
  - PayPal dispute
  - M-Pesa reversal request
- **Chargeback response:**
  - Evidence compilation
  - Representment submission
  - Arbitration preparation
- **Win/loss tracking:**
  - Chargeback win rate
  - Loss rate and analysis
  - Fraud pattern identification

---

## Page 1.17 — System Health & Operations

**Purpose:** Platform infrastructure monitoring, incident management, and operational readiness.

### Section 1.17.1 — System Status Dashboard

- **Service status page:**
  - M-Pesa integration: Healthy, Degraded, Down
  - PesaLink integration: Healthy, Degraded, Down
  - RTGS/KEPSS: Healthy, Degraded, Down
  - EFT/ACH: Healthy, Degraded, Down
  - SWIFT: Healthy, Degraded, Down
  - EAPS: Healthy, Degraded, Down
  - PAPSS: Healthy, Degraded, Down
  - PayPal: Healthy, Degraded, Down
  - Visa Direct: Healthy, Degraded, Down
  - Mastercard Send: Healthy, Degraded, Down
  - Core banking system: Healthy, Degraded, Down
  - Database: Healthy, Degraded, Down
  - API gateway: Healthy, Degraded, Down
  - Web application: Healthy, Degraded, Down
  - Mobile app: Healthy, Degraded, Down
- **Uptime percentage:**
  - Per-service uptime (target: 99.9%)
  - MTTR (Mean Time To Recovery)
  - MTBF (Mean Time Between Failures)

### Section 1.17.2 — Incident Management

- **Incident log:**
  - All incidents with severity, start time, end time, duration, impact
  - Incident categorization: rail downtime, API failure, database issue, network issue, third-party outage
- **Incident response:**
  - Auto-alert to on-call team
  - Incident war room coordination
  - Status page update
  - Customer communication
  - Post-incident review
- **Post-mortem documentation:**
  - Root cause analysis
  - Timeline of events
  - Lessons learned
  - Prevention measures
  - Action items with owners

### Section 1.17.3 — Capacity Planning

- **Resource utilization:**
  - CPU, memory, disk, network
  - Database connection pool
  - API rate limit utilization
  - Queue depth
- **Scaling triggers:**
  - Auto-scaling rules
  - Manual scaling capability
  - Load testing schedule
  - Capacity forecast

---

## Cross-Cutting Features (All Dashboard 1 Pages)

| Feature | Description |
|---------|-------------|
| **Global Search** | Universal search across transactions, customers, accounts, rails, settings, documents |
| **Advanced Notifications** | Real-time alerts via in-app, SMS, email, Slack, WhatsApp Business, PagerDuty, webhook |
| **Dark/Light Mode** | Theme toggle for user preference, with auto-detect from OS |
| **Multi-Language Support** | English (default), Swahili, French, Arabic, Portuguese, Luganda, Kinyarwanda, Hausa, Yoruba, Zulu, Amharic |
| **Accessibility (a11y)** | WCAG 2.1 AA compliance, keyboard navigation, screen reader support, high contrast mode, font sizing |
| **Mobile Responsive** | Full functionality on tablet and mobile devices, PWA support |
| **Keyboard Shortcuts** | Power-user shortcuts for common actions (Ctrl+T new transfer, Ctrl+R reconciliation, etc.) |
| **Data Export** | One-click export of any table/view to CSV, Excel, PDF, JSON, XML |
| **Audit Trail** | Immutable log of all user actions across the platform with cryptographic integrity |
| **Help & Support** | Contextual help, chat support, knowledge base, video tutorials, community forum |
| **Multi-Currency Display** | Primary currency selector (KES default) with secondary currency display |
| **Timezone Support** | EAT (Nairobi, default), CAT, WAT, GMT, ET, CET — per-user preference |
| **Date Format** | DD/MM/YYYY (default for Kenya), MM/DD/YYYY, YYYY-MM-DD |
| **Number Format** | Kenyan format (1,000,000.00), European format (1.000.000,00), Indian format (10,00,000.00) |
| **Session Management** | Auto-lock after inactivity, concurrent session control, remote logout |
| **Role-Based Access** | Super Admin, Admin, Operations Manager, Operations Analyst, Compliance Officer, Treasury Manager, Finance Manager, Auditor, Read-Only |
| **Two-Factor Authentication** | SMS OTP, Email OTP, Authenticator App, Hardware Token, Biometric |
| **Data Residency** | Primary data storage in Kenya, with DR in Rwanda or South Africa, GDPR-compliant EU storage |
| **API-First Design** | Every UI action available via API for automation and integration |

---

## Suggested Tech Stack (Africa-Optimized)

| Layer | Technology |
|-------|------------|
| **Frontend** | Angular v21, Bootstrap 5, Bootstrap Icons, RxJS, NgRx |
| **State Management** | NgRx Store + Effects |
| **Charts & Visualization** | Apache ECharts (supports African map projections), Chart.js |
| **Tables** | AG Grid Enterprise |
| **Forms** | Reactive Forms + Custom validators |
| **Real-time** | WebSockets (Socket.io) with fallback to SSE for low-bandwidth |
| **Offline Support** | Service Workers, IndexedDB for offline transaction queueing |
| **Theming** | CSS Custom Properties for light/dark, plus high contrast |
| **Maps** | Leaflet.js with OpenStreetMap (offline tile support for rural areas) |
| **Backend** | Node.js/NestJS (primary), Java Spring Boot (for core banking integration) |
| **Database** | PostgreSQL (transactional, primary), MongoDB (logs, unstructured data), Redis (cache, session), TimescaleDB (time-series metrics) |
| **Message Queue** | Apache Kafka (primary), RabbitMQ (fallback for low-latency) |
| **Search** | Elasticsearch |
| **Monitoring** | Grafana + Prometheus + Loki |
| **Mobile SDK** | Flutter (for cross-platform mobile app with offline capability) |
| **M-Pesa Integration** | Safaricom Daraja API v2 |
| **PesaLink Integration** | IPSL API |
| **KRA Integration** | eTIMS API, iTax API |
| **Document Storage** | MinIO (S3-compatible, on-premise for data sovereignty) |
| **Identity** | Keycloak with Kenyan ID verification integration |

---

This completes the comprehensive, Africa-first Dashboard 1 for PayMo — covering every aspect of bank-to-bank transactions with deep localization for Kenyan, East African, and broader African markets, while maintaining full global capability.






















---


## Cross-Cutting Features (Both Dashboards)

These features should be available globally across both dashboards:

| Feature | Description |
|---------|-------------|
| **Global Search** | Universal search across transactions, clients, invoices, settings |
| **Advanced Notifications** | Real-time alerts via in-app, email, SMS, Slack, webhook |
| **Dark/Light Mode** | Theme toggle for user preference |
| **Multi-Language Support** | i18n for English, French, Spanish, Arabic, Swahili, etc. |
| **Accessibility (a11y)** | WCAG 2.1 AA compliance, keyboard navigation, screen reader support |
| **Mobile Responsive** | Full functionality on tablet and mobile devices |
| **Keyboard Shortcuts** | Power-user shortcuts for common actions |
| **Data Export** | One-click export of any table/view to CSV, Excel, PDF |
| **Audit Trail** | Immutable log of all user actions across the platform |
| **Help & Support** | Contextual help, chat support, knowledge base, video tutorials |

---

## Suggested Tech Stack (Aligned with Your Angular v21 Setup)



---

This outline gives  a production-grade, enterprise-level blueprint that rivals PesaLink, Plaid, Payoneer, and the top BaaS platforms in the market. Each page is designed with real operational workflows, compliance requirements, and scalability in mind. 

now i want you to design using the master css using this theme as the main default theme, with the styled and design in bootstrap and custom css and custom js , make it well designed well with the icons and the cards and tabs exactly as the theme in the pic sample
we are making the dashboard with sidebar and collapsable to show icons with hover icons 

create relevant mini tabs whenever necessary and relevant mini pop ups to avoid dead end placeholder every button or link should be completed by events like loading etc
don’t leave blanks or placeholder make everything completed
create mini modal pop ups, medium-large sized pop ups, medium pop up modals upon clicking buttons for the next step section 
create tabs within the modal if the steps requires multiple steps
create multistep modals like for making payments like inlcude relevant steps and steps for security feature like pin or passkey etc and conformations, event like button clicking , cards tables and sections to have UI/UX design like 
no dead ends, make everything completed use little or less toastas (limit them not everything should be toasted)
use the theme with bootstrap inline styles
us ethe master styles  and  custom js

make it comprohensive and functional, responsive on mobile screen
 
make the root theme constant to maintain the theme
| Feature                    | Description                                                        |
| -------------------------- | ------------------------------------------------------------------ |
| **Global Search**          | Universal search across transactions, clients, invoices, settings  |
| **Advanced Notifications** | Real-time alerts via in-app, email, SMS, Slack, webhook            |
| **Dark/Light Mode**        | Theme toggle for user preference                                   |
| **Multi-Language Support** | i18n for English, French, Spanish, Arabic, Swahili, etc.           |
| **Accessibility (a11y)**   | WCAG 2.1 AA compliance, keyboard navigation, screen reader support |
| **Mobile Responsive**      | Full functionality on tablet and mobile devices                    |
| **Keyboard Shortcuts**     | Power-user shortcuts for common actions                            |
| **Data Export**            | One-click export of any table/view to CSV, Excel, PDF              |
| **Audit Trail**            | Immutable log of all user actions across the platform              |
| **Help & Support**         | Contextual help, chat support, knowledge base, video tutorials     |


make the page below 

as a full html page with in page custom css and custom js and create a master style file master css
p

give a single combined html page alone for thia modifications






so this is my dashboad pages
correct the few errors of card alinment, resposive content on small device should not crump up or squeeze
then use modals pop ups where relevant, no blank no dead ends no empty place holders
make it responsive
add missing modals

now i want you to design using the master css using this theme as the main default theme, with the styled and design in bootstrap and custom css and custom js , make it well designed well with the icons and the cards and tabs exactly as the theme in the pic sample
we are making the dashboard with sidebar and collapsable to show icons with hover icons 

create relevant mini tabs whenever necessary and relevant mini pop ups to avoid dead end placeholder every button or link should be completed by events like loading etc
don’t leave blanks or placeholder make everything completed
create mini modal pop ups, medium-large sized pop ups, medium pop up modals upon clicking buttons for the next step section 
create tabs within the modal if the steps requires multiple steps
create multistep modals like for making payments like inlcude relevant steps and steps for security feature like pin or passkey etc and conformations, event like button clicking , cards tables and sections to have UI/UX design like 
no dead ends, make everything completed use little or less toastas (limit them not everything should be toasted)
use the theme with bootstrap inline styles
use the master styles  and  custom js

make it comprohensive and functional, responsive on mobile screen

in the same manner and design using the theme and master css

make it comprehensive, reduce the use of toastas, no broken links no empty sections
use modals, tabs, mutistep modals pop ups no blanks, no empty links no empty buttons
use over 20 modals
make it comprehesive reduce the use of toastas, no broken links no empty sections
this is the admins side dashboard so allow permissions and editable fields, data, records and sections relevantly
design the next page

 Here is the exhaustive outline for **Page 18 — Account Settings, Details, Profile & Administration**:

---

# PAGE 18 — ACCOUNT SETTINGS, DETAILS, PROFILE & ADMINISTRATION

**Purpose:** Centralized command center for managing user identity, business profile, security posture, notification preferences, team access, API credentials, billing, and platform-wide administrative controls. Serves as the single source of truth for all account-level configuration across individual users, business entities, and platform administrators.

---

## TAB SECTION 18.1 — PERSONAL PROFILE & IDENTITY

### 18.1.1 — Profile Overview Card
- **Avatar & visual identity:** Profile photo upload with crop/zoom editor, fallback initials avatar with custom color selection, business logo display (if business account), cover banner image for business profiles
- **Display name & handle:** Full legal name, preferred display name, unique PayMo handle (@username), public profile URL
- **Account tier badge:** Basic, Verified, Premium, Enterprise with tier benefits tooltip
- **Profile completeness progress bar:** Percentage complete with missing items checklist (photo, phone verify, 2FA, KYC, etc.)
- **Quick actions:** Edit profile, View public profile, Download profile data (GDPR/ODPC portability), Share profile QR code

### 18.1.2 — Identity Verification & KYC
- **Document upload center:** National ID (Huduma Namba / old ID / passport / alien ID / driving license) front and back, selfie with liveness detection (blink, turn head, smile challenge), proof of address (utility bill, bank statement, tenancy agreement, employer letter)
- **Verification status tracker:** Pending upload → Under Review → Verified → Rejected → Resubmit, with timestamp and reviewer notes per stage
- **Verification level progression:** Level 1 (email/phone) → Level 2 (ID + selfie) → Level 3 (address proof) → Level 4 (enhanced due diligence), each level unlocking higher limits and features
- **Re-verification triggers:** Document expiry alerts (90/60/30/7 days), name change workflow, address change workflow, annual re-verification requirement for high-tier accounts
- **Biometric enrollment:** Fingerprint setup (mobile), Face ID setup (iOS/Android), Voice print (optional), Biometric usage log and device management

### 18.1.3 — Contact Information
- **Primary contact:** Email (verified/unverified badge, change workflow with OTP confirmation), phone number (with country code selector, SIM registration verification, change workflow with 72-hour cooling-off period)
- **Secondary/backup contacts:** Backup email, emergency contact (name, relationship, phone), trusted device phone number
- **Communication preferences:** Preferred language (English, Swahili, French, Arabic, Portuguese, Luganda, Kinyarwanda), preferred timezone (EAT/CAT/WAT/GMT/ET/CET), date format (DD/MM/YYYY, MM/DD/YYYY, YYYY-MM-DD), number format (Kenyan 1,000,000.00, European 1.000.000,00, Indian 10,00,000.00)
- **Address book:** Primary residence, business address, billing address, shipping address (for card delivery), address verification status per entry, GPS coordinate capture for delivery optimization

### 18.1.4 — Professional & Business Identity
- **Occupation & income:** Employment status (employed, self-employed, business owner, unemployed, student, retired), employer name and sector, monthly income range, source of income declaration
- **Business linkage:** Linked business accounts (if business owner/employee), role within each business (Owner, Director, Employee, Accountant), business verification status per linkage
- **Tax identity:** KRA PIN (verified/unverified, auto-link to iTax), TIN for other jurisdictions, tax residency declaration (Kenya resident, non-resident, dual resident), FATCA/CRS self-certification

---

## TAB SECTION 18.2 — SECURITY CENTER

### 18.2.1 — Authentication Methods
- **Password management:** Current password strength meter (weak/medium/strong), password change with old password verification, password history enforcement (no last 5 passwords), password expiry policy (30/60/90/never days), breached password detection (HaveIBeenPwned integration)
- **Multi-factor authentication (MFA):** Status toggle with enforcement level (optional, recommended, mandatory), available methods: SMS OTP, Email OTP, Authenticator app (Google Authenticator, Authy, Microsoft Authenticator — QR code setup with secret key backup), Hardware security key (YubiKey, FIDO2/WebAuthn — register multiple keys), Biometric (fingerprint, Face ID), Push notification approval (PayMo app)
- **MFA backup & recovery:** Backup codes generation (10 single-use codes), download/print backup codes, regenerate backup codes (invalidates old), recovery email/phone setup, trusted contact for account recovery
- **Login method preferences:** Default login method selection, passwordless login toggle (magic link, biometric only), remember device duration (1 day, 7 days, 30 days, never), trusted device list with revoke capability

### 18.2.2 — Device & Session Management
- **Active sessions dashboard:** All logged-in devices with device name, type (mobile/desktop/tablet), OS, browser/app, IP address, geolocation (city/country), login timestamp, last activity timestamp, session duration
- **Session controls:** Remote logout any individual session, logout all other sessions, force password reset on suspicious session, mark device as trusted/untrusted
- **Device fingerprinting:** Device trust score, new device alert configuration, impossible travel detection (login from Nairobi and London within 1 hour), device change verification requirement
- **Login history:** 90-day searchable log (date, time, IP, device, location, method, success/failure), failed login attempt tracking with auto-lockout, export login history (CSV/PDF)

### 18.2.3 — Security Alerts & Monitoring
- **Alert configuration:** New device login, password changed, MFA disabled/modified, email/phone changed, large transaction, international login, suspicious activity pattern, SIM swap detection, account freeze/unfreeze
- **Alert delivery channels:** In-app notification, SMS, email, WhatsApp, push notification — configurable per alert type
- **Security score:** Dynamic score (0-100) based on: password strength, MFA enabled, backup codes saved, trusted devices only, recent security review, no active alerts — with improvement recommendations
- **Security audit:** Last security review date, recommended actions checklist, security checklist completion percentage, annual security health check reminder

### 18.2.4 — Account Protection Controls
- **Transaction limits:** Per-transaction limit (configurable by type: transfer, payment, withdrawal, FX), daily aggregate limit, weekly aggregate limit, monthly aggregate limit, limit increase request with justification and supporting documents
- **Beneficiary controls:** Cooling-off period for new beneficiaries (0/24/48/72 hours), beneficiary whitelist mode (only pre-approved beneficiaries), beneficiary change notification, beneficiary approval workflow for business accounts
- **Geographic restrictions:** Allow transactions only from specific countries, block high-risk countries, home country lock (transactions only from Kenya unless travel mode enabled), travel mode pre-declaration with dates and destinations
- **Time-based restrictions:** Allow transactions only during specified hours, block weekend transactions (configurable), holiday transaction exceptions
- **Account freeze:** Self-freeze toggle (immediate, with unfreeze requiring MFA + identity verification), freeze reason selection, scheduled auto-unfreeze, freeze notification to all contacts

---

## TAB SECTION 18.3 — NOTIFICATION & COMMUNICATION PREFERENCES

### 18.3.1 — Notification Channel Management
- **Channel setup:** In-app push (primary, always on for critical), SMS (primary number, backup number, international number for diaspora), email (primary, billing, alerts — separate addresses), WhatsApp Business (opt-in with number verification), Slack/Teams integration (webhook URL, channel selection), webhook endpoints (custom URL per event category)
- **Channel health status:** Delivery success rate per channel, last successful delivery timestamp, channel verification status, failed delivery retry configuration

### 18.3.2 — Event-Based Notification Tuning
- **Transaction events:** Successful payment (on/off), failed payment (on/off), large transaction threshold alert, international transaction, recurring payment processed, refund received, chargeback alert, dispute update
- **Security events:** Login from new device, password changed, MFA enabled/disabled, email/phone changed, suspicious activity detected, account frozen/unfrozen, API key rotated
- **Business events:** Invoice paid, invoice overdue, payroll executed, payroll failed, bulk disbursement completed, settlement received, report ready, compliance deadline approaching
- **Marketing & updates:** Promotional offers, new features, partner offers, newsletter, product tips, survey invitations — all with granular opt-in/opt-out per category
- **Frequency controls per event:** Real-time, hourly digest, daily digest (time selection), weekly digest (day selection), monthly digest, only critical, completely off

### 18.3.3 — Quiet Hours & Do Not Disturb
- **Schedule configuration:** Start time, end time, timezone, days of week (weekdays only, weekends only, all days, custom)
- **Critical override:** Security alerts and fraud warnings always break through quiet hours
- **Vacation mode:** Temporarily pause non-critical notifications with auto-resume date
- **Emergency contact bypass:** Designated emergency contacts can override quiet hours

---

## TAB SECTION 18.4 — TEAM & ACCESS MANAGEMENT (Business Accounts)

### 18.4.1 — Team Member Directory
- **Member listing:** All team members with avatar, name, email, role, department, status (active/invited/deactivated), last login, MFA status, approval limit
- **Quick actions:** Edit role, Reset MFA, Force password reset, Deactivate, Delete, View activity log, Transfer ownership (for Owner role)
- **Member profile drawer:** Full profile with permissions matrix, recent activity, assigned tasks, pending approvals, security status

### 18.4.2 — Role & Permission Builder
- **Predefined roles:** Owner (full access, cannot be restricted), Admin (user management, settings, view all, cannot delete business), Finance Manager (collections, disbursements, payroll, reports, no user management), Accountant (bookkeeping, reconciliation, reports, read-only execution), HR Manager (payroll, employee data, benefits, leave), Sales Manager (invoicing, collections, customer management, no disbursements), Procurement Officer (supplier management, purchase orders, invoice processing, payment initiation), Viewer (read-only dashboard, no execution), Developer (API access, webhook management, sandbox only), Compliance Officer (audit logs, regulatory reports, screening results, read-only execution)
- **Custom role builder:** Module access toggles (Collections, Disbursements, Payroll, Invoicing, Treasury, Reports, Settings, API, Cards, Virtual Accounts, FX, Compliance), action permissions per module (View, Create, Edit, Delete, Approve, Execute, Export, Configure), data scope (All data, Department-only, Own data, None), feature limits (max approval amount, max transaction amount, max batch size, max API calls), time restrictions (business hours, weekend access, holiday access), geographic restrictions (IP whitelist, country whitelist)
- **Permission preview:** Simulate what a user with this role would see/do, permission conflict detection, role cloning and template saving

### 18.4.3 — Invitation & Onboarding Workflow
- **Invite member:** Email, role selection, department, approval limit, MFA requirement toggle, custom message, expiry (24 hours, 7 days, 30 days)
- **Invitation tracking:** Sent, Opened, Accepted, Expired, Revoked statuses, resend invitation, bulk invite via CSV
- **First-login mandatory setup:** MFA enrollment, password creation, terms acceptance, department confirmation, approval limit acknowledgment
- **Offboarding checklist:** Revoke all sessions, disable API keys, reassign pending approvals, transfer ownership of recurring tasks, archive personal data (retain audit logs per regulation), final access date log

### 18.4.4 — Approval Workflows & Authorization Matrix
- **Amount-based approval tiers:** <KES 100,000 (single approver), KES 100,000-1,000,000 (dual approval), >KES 1,000,000 (triple approval + compliance), equivalent tiers in USD/EUR/GBP
- **Category-based rules:** Payroll auto-approved within variance, capex requires procurement sign-off, international transfers require compliance pre-approval, bulk disbursements >100 beneficiaries require director sign-off
- **Delegation rules:** Auto-delegate to backup approver during absence (leave, travel, sick), manual delegation with date range, delegation history and revocation
- **Approval deadline & escalation:** 24-hour default deadline, auto-reminder at 50% and 80% of deadline, auto-escalation to manager after deadline, escalation chain configuration

---

## TAB SECTION 18.5 — API & INTEGRATION SETTINGS

### 18.5.1 — API Credential Management
- **Project/workspace list:** All API projects with name, environment (sandbox/production), status, created date, last activity
- **Credential details per project:** Client ID (masked, reveal toggle), Client Secret (fully masked, regenerate button), API key (masked, rotate schedule), OAuth 2.0 redirect URIs, allowed IP ranges, allowed origins (CORS)
- **Credential lifecycle:** Generate new, Rotate (grace period with old key valid for 24 hours), Revoke (immediate invalidation), Expiry tracking with alerts (30/7/1 day warnings)
- **Scope configuration:** Granular permission toggles per API endpoint category (payments, disbursements, payroll, collections, virtual accounts, FX, webhooks, read-only)

### 18.5.2 — Webhook Endpoint Management
- **Endpoint directory:** All registered webhook URLs with event types subscribed, delivery success rate, average latency, last delivery timestamp, status (active/paused/failing)
- **Endpoint configuration:** URL (HTTPS-only validation), event type subscription toggles, payload format (JSON/XML/form-encoded), custom headers (authentication), retry policy (max retries, backoff strategy), timeout setting
- **Delivery log:** Last 1,000 deliveries with timestamp, event type, payload size, HTTP status, response time, retry count, full request/response inspectable
- **Testing tools:** Send test event, verify signature validation, inspect payload structure, simulate retry behavior, load test with 100 concurrent events

### 18.5.3 — Third-Party Integrations
- **Connected apps directory:** All active integrations with logo, name, status, permissions granted, data access scope, connected date, last sync
- **Integration types:** Accounting (QuickBooks, Xero, Sage, SAP, Oracle NetSuite), E-commerce (Shopify, WooCommerce, Magento, PrestaShop), CRM (Salesforce, HubSpot, Zoho), HR (Workday, BambooHR), Communication (Slack, Teams, WhatsApp Business API), Analytics (Google Analytics, Mixpanel), Identity (Azure AD, Google Workspace, Okta)
- **Per-integration controls:** Sync frequency, data scope (read-only vs. read-write), field mapping configuration, error log, pause/resume sync, disconnect with data deletion confirmation
- **Integration health dashboard:** Sync status, last successful sync, error rate, data freshness, API quota utilization

---

## TAB SECTION 18.6 — BILLING, FEES & SUBSCRIPTION

### 18.6.1 — Current Plan & Usage
- **Plan card:** Current tier (Starter/Growth/Enterprise/Custom), monthly/annual billing cycle, next billing date, days remaining, plan features checklist with used vs. included quotas
- **Usage meters:** API calls (current vs. limit), transactions processed (current vs. limit), active users (current vs. limit), storage used (current vs. limit), webhook deliveries (current vs. limit)
- **Upgrade/downgrade path:** Side-by-side plan comparison, feature matrix, prorated cost calculation, downgrade impact warning (data loss, feature loss), upgrade immediate activation

### 18.6.2 — Payment Methods & Billing
- **Payment methods:** M-Pesa (primary, auto-pay setup), bank transfer (PesaLink/EFT/RTGS), debit/credit card (Visa/Mastercard, 3D Secure), PayMo wallet balance
- **Billing address:** Separate from business address, tax invoice requirements, e-TIMS integration for tax invoice generation
- **Invoice history:** All invoices with number, date, amount, status (paid/pending/overdue), PDF download, payment confirmation, dispute invoice
- **Auto-pay configuration:** Enable/disable, preferred method, backup method, failed payment retry (3 attempts), low balance alert before billing

### 18.6.3 — Fee Schedule & Cost Transparency
- **Current fee schedule:** Per-transaction fees by rail (M-Pesa, PesaLink, RTGS, EFT, SWIFT, etc.), FX spread by currency pair, monthly platform fee, API overage fees, support tier fees
- **Fee calculator:** Interactive tool — select transaction type, amount, currency, rail → instant fee calculation with breakdown
- **Volume discounts:** Current tier, next tier threshold, projected savings at next tier, annual prepay discount (2 months free)
- **Cost analytics:** Monthly spend trend, spend by category (rails, FX, API, support), cost per transaction trend, savings from bulk vs. individual pricing

---

## TAB SECTION 18.7 — DATA PRIVACY & COMPLIANCE

### 18.7.1 — Data Privacy Controls
- **Consent management:** Granular consent toggles per data type (profile, transactions, location, device, contacts, photos), consent history with date and version, consent withdrawal with impact disclosure
- **Data sharing preferences:** Share with PayMo partners (on/off), share for product improvement (on/off), share for marketing (on/off), anonymized analytics participation (on/off)
- **Marketing preferences:** Email marketing, SMS marketing, push marketing, partner offers, personalized recommendations — all individually togglable
- **Cookie & tracking preferences:** Essential (required), Functional, Analytics, Marketing — with detailed cookie list and purpose explanation

### 18.7.2 — Data Subject Rights (GDPR/ODPC)
- **Right to access:** Request full data package (profile, transactions, logs, documents), delivery method (download link, email, physical mail), processing time tracker (30-day SLA)
- **Right to rectification:** Request data correction with evidence upload, correction workflow tracking, notification when corrected
- **Right to erasure (right to be forgotten):** Account deletion request with impact assessment (what will be deleted, what retained per regulation), cooling-off period (30 days), irreversible deletion confirmation, data retention exceptions (regulatory 7-year requirement)
- **Right to portability:** Export data in standard formats (JSON, CSV, OFX, MT940), structured machine-readable format, direct transfer to another provider (where technically feasible)
- **Right to restrict processing:** Temporarily pause data processing while dispute resolution pending, restricted mode features available

### 18.7.3 — Regulatory Compliance Status
- **Compliance dashboard:** KYC/KYB status, AML monitoring status, tax compliance (KRA), data protection (ODPC), PCI DSS (if card processing), CBK licensing status, annual audit status
- **Filing calendar:** Upcoming regulatory deadlines (KRA, CBK, ODPC, county permits), automatic reminders (90/60/30/7 days), filing status tracking, document upload for each filing
- **Compliance score:** Dynamic score (0-100) based on document currency, filing timeliness, regulatory standing, risk profile stability — with improvement recommendations and feature unlocks tied to score

---

## TAB SECTION 18.8 — PLATFORM ADMINISTRATION (Super Admin Only)

### 18.8.1 — System Configuration
- **Global settings:** Platform name, branding (logo, colors, favicon), default language, default currency, default timezone, maintenance mode toggle, registration open/closed, invitation-only toggle
- **Feature toggles:** Enable/disable modules (Collections, Disbursements, Payroll, Invoicing, FX, Cards, Virtual Accounts, API, Sandbox), beta features per tenant, experimental features with opt-in
- **Rate limits & quotas:** Global API rate limit, per-tenant rate limit, per-user rate limit, file upload size limit, batch processing size limit, webhook timeout default
- **Security policies:** Global password policy, global MFA enforcement, session timeout default, account lockout policy, IP blacklist (global), country blacklist (global)

### 18.8.2 — Tenant & Client Management
- **Tenant directory:** All business tenants with name, status, plan, created date, last activity, user count, transaction volume, compliance score
- **Tenant actions:** View tenant dashboard (impersonate), Suspend tenant, Activate tenant, Delete tenant (with data archive), Migrate tenant plan, Assign dedicated support agent
- **Tenant onboarding approval:** Review and approve new tenant registrations, KYB document review, risk assessment override, custom plan negotiation
- **White-label configuration per tenant:** Custom domain, SSL certificate, custom branding, custom email templates, custom mobile app build

### 18.8.3 — Audit & System Logs
- **System audit log:** All platform-level actions with immutable hash, timestamp, actor, action, target, before/after values, IP, device
- **Log search & filter:** By date range, actor, action type, target type, severity, keyword search
- **Log export:** CSV, JSON, SIEM-compatible format (CEF, LEEF), automated daily export to SIEM
- **Log retention policy:** Hot storage (30 days), warm storage (90 days), cold archive (7 years), auto-purge configuration

### 18.8.4 — Backup & Disaster Recovery
- **Backup status:** Last backup timestamp, backup size, backup type (full/incremental), backup location (primary, DR site, cloud), verification status
- **Backup scheduling:** Daily full backup, hourly incremental, real-time transaction log shipping
- **Restore testing:** Last restore test date, restore test results, scheduled restore drills
- **Disaster recovery runbook:** DR plan document, RTO/RPO targets, failover procedures, contact tree, emergency communication templates

---

## TAB SECTION 18.9 — ACCOUNT LIFECYCLE

### 18.9.1 — Account Status Management
- **Status transitions:** Active → Suspended → Dormant → Closed, with valid transition paths and required actions per transition
- **Self-suspension:** Temporary suspension with reason (travel, security concern, account review), scheduled auto-reactivation, reactivation workflow (MFA + identity verification)
- **Dormancy management:** Dormancy warning (90 days no activity), reactivation incentive, dormancy fee disclosure, auto-closure timeline (2 years)

### 18.9.2 — Account Closure
- **Closure request form:** Reason selection (switching provider, business closed, dissatisfied, security concern, other), satisfaction survey, retention offer presentation
- **Pre-closure checklist:** Outstanding balance settlement, pending transactions completion, active subscriptions cancellation, recurring payments cancellation reminder, data export offer, beneficiary notification
- **Closure execution:** Balance transfer to nominated account (M-Pesa/bank/card), final statement generation, data retention confirmation (7 years per CBK), closure certificate, 30-day reactivation window
- **Post-closure:** Data archive status, regulatory retention compliance, permanent deletion after retention period, right to be forgotten fulfillment confirmation

### 18.9.3 — Account Recovery
- **Forgotten credentials:** Email reset, phone reset, security questions (if configured), trusted contact recovery, identity verification recovery (ID + selfie)
- **Compromised account recovery:** Immediate freeze, investigation workflow, credential reset, session revocation, transaction review, fraud report filing, reactivation after clearance
- **Deceased account holder:** Next of kin claim process, death certificate upload, legal heir documentation, court order upload, account balance transfer to estate, closure with estate documentation

---

**END OF PAGE 18 OUTLINE**