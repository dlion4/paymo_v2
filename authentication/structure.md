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
•	Page 55: Account Type Selection (Post-Login)
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
