I'll read those two specification documents first to understand your BAAS architecture, then create a focused, exhaustive outline for Dashboard 5.
I've read both documents. Here's the exhaustive outline for **Dashboard 5: Cards, Virtual Credit & Debit Center** — designed as a complete, self-contained BAAS card management system with no overlap with Dashboards 1–4.

---

# DASHBOARD 5: PAYMO CARD CENTER — Cards, Virtual Credit & Debit Management

**Purpose:** Dedicated dashboard for all card-related financial services — physical and virtual debit cards, virtual credit cards, prepaid cards, corporate card programs, card controls, BIN management, tokenization, and card-linked analytics. Serves individual consumers, SMEs, corporates, and fintech partners who need to issue, manage, and monitor card products.

---

## PAGE 5.1 — CARD COMMAND CENTER

### Section 5.1.1 — Card Portfolio Overview
- **Active cards summary:** Total cards issued (physical + virtual), Active vs. frozen vs. expired vs. cancelled count, Cards by type: debit, credit, prepaid, corporate, Total available credit across all credit cards, Total prepaid balance across all prepaid cards, Daily/monthly spending across all cards
- **Quick-action card grid:** Each card displayed as a visual card widget with last 4 digits, cardholder name, expiry, card type icon, Current balance / available credit / prepaid balance per card, Tap-to-reveal full PAN (with biometric/PIN gate), One-tap freeze/unfreeze toggle, Copy card number button (for virtual cards), Show/hide CVV toggle with timer auto-hide
- **Recent card activity:** Last 10 transactions across all cards with merchant name, amount, status, timestamp, Category icons (dining, fuel, groceries, online, travel, etc.), Tap-to-view full transaction details and receipt
- **Spending alerts & notifications:** Real-time push for every transaction, Large transaction alerts (configurable threshold), International transaction alerts, Declined transaction alerts with reason, Card-not-present (CNP) fraud alerts, Contactless payment limit reached alert

### Section 5.1.2 — Card Health & Status Dashboard
- **Card status indicators:** Green (active and ready), Amber (expiring within 60 days, approaching limit, low prepaid balance), Red (frozen, expired, compromised, declined repeatedly), Blue (newly issued, pending activation)
- **Expiry management:** Cards expiring in next 90 days with countdown, Auto-renewal status per card, Renewal request initiation, New card delivery tracking
- **Security posture score:** Per-card security score (0-100) based on: PIN changes recency, 3D Secure enrollment, Contactless enabled/disabled, Online transaction history, Geolocation consistency, Device binding status, Score improvement recommendations

### Section 5.1.3 — Spending Analytics & Budgeting
- **Card spending dashboard:** Today's spend, this week's spend, this month's spend per card and aggregated, Spend by category: dining, transport, shopping, utilities, entertainment, healthcare, education, travel, others with pie chart, Spend by channel: POS, ATM, online, contactless, mobile wallet, recurring payments
- **Budget controls:** Monthly spending cap per card, Category-level budgets with progress bars, Budget overrun alerts and auto-block options, Rollover unused budget to next month toggle, Budget vs. actual comparison with variance analysis
- **Merchant analytics:** Top merchants by spend and frequency, Merchant-level spending trends, Duplicate merchant detection (same merchant, multiple card entries), Merchant category code (MCC) analysis

### Section 5.1.4 — Card Quick Actions
- **Instant actions:** Freeze/unfreeze card (with reason selection: lost, stolen, suspected fraud, temporary, other), Report lost/stolen (immediate permanent block, replacement order), Request replacement (damaged, lost, expired), Change PIN (with old PIN verification or OTP fallback), Reset PIN (via OTP to registered phone/email), Update contactless limit, Toggle online transactions, Toggle international transactions, Toggle ATM withdrawals, Set temporary spending limit
- **Payment actions:** Pay card bill (for credit cards), Top-up prepaid card, Transfer between cards (debit to prepaid, prepaid to prepaid), Card-to-M-Pesa transfer, Card-to-bank transfer

---

## PAGE 5.2 — PHYSICAL DEBIT CARD MANAGEMENT

### Section 5.2.1 — Card Issuance & Ordering
- **New card application:** Card type selection: Standard Debit, Premium Debit, Student Debit, Senior Citizen Debit, Business Debit, Card design selection: Standard designs, Custom photo upload for personalized cards, Branded designs for corporate programs, Delivery address: Primary address, alternate address, branch pickup, Delivery method: Standard mail (5-7 days), Express courier (1-2 days), Branch pickup (same day after printing), Card personalization: Name embossing, signature panel, EMV chip, contactless symbol
- **Application tracking:** Real-time status: Application received → Under review → Approved → Personalization → Dispatched → Delivered, Estimated delivery date with courier tracking link, Delivery OTP requirement (card only released with OTP), Failed delivery handling: reschedule, branch hold, address update
- **Bulk card ordering (corporate):** Employee card bulk upload (CSV: name, employee ID, department, spending limit), Corporate branding: Logo, colors, card design, Department-based card numbering scheme, Batch tracking with per-card status, Centralized delivery to HR or direct to employee

### Section 5.2.2 — Card Activation & PIN Management
- **Activation methods:** In-app activation: Scan card QR code or enter last 4 digits + OTP, IVR activation: Call dedicated number, enter card number + OTP, Branch activation: Present ID and card at branch, ATM activation: First PIN set at any partner ATM
- **PIN setup:** 4-digit PIN creation with strength check (no sequential, no repeated digits), PIN confirmation, Biometric binding: Fingerprint or face ID for PIN-less high-value transactions, PIN change: Anytime via app with old PIN or OTP, Forgotten PIN reset: OTP + ID verification + security questions
- **Card binding:** Link to PayMo wallet for seamless top-up, Link to M-Pesa for direct card-to-mobile transfers, Link to bank accounts for funding, Set default funding source priority

### Section 5.2.3 — Physical Card Controls
- **Transaction controls:** Daily spending limit (configurable per card), Per-transaction limit, Contactless transaction limit (tap-to-pay cap), Online transaction toggle, International transaction toggle (with country whitelist/blacklist), ATM withdrawal toggle, Cashback at POS toggle, Recurring payment toggle
- **Geographic controls:** Enable/disable transactions by country/region, Kenya-only mode, East Africa mode, Global mode, Geo-fencing: Block transactions outside defined radius from home/work, Travel mode: Pre-declare travel dates and destinations to prevent blocks
- **Time-based controls:** Transaction allowed hours (e.g., 6 AM – 11 PM), Weekend transaction toggle, Holiday transaction exceptions
- **Merchant controls:** Block by MCC category (gambling, alcohol, adult content), Allowlist specific merchants, Blocklist specific merchants, Subscription merchant management

### Section 5.2.4 — Card Replacement & Cancellation
- **Replacement reasons:** Lost, stolen, damaged (magnetic stripe, chip, contactless), Expired, Compromised (fraud suspicion), Name change, Design upgrade, Damaged card photo upload for verification
- **Replacement process:** Request initiation with reason, Old card immediate block (for lost/stolen/compromised), New card personalization and dispatch tracking, Old card balance transfer to new card, Linked recurring payments auto-migration notification, Card number change handling for subscriptions
- **Cancellation:** Permanent cancellation with reason, Balance settlement: Transfer to wallet, M-Pesa, or bank account, Recurring payment cancellation reminder, Cancellation confirmation with certificate of closure, Reactivation window: 30 days to reactivate before permanent closure

---

## PAGE 5.3 — VIRTUAL DEBIT CARD CENTER

### Section 5.3.1 — Virtual Card Creation & Lifecycle
- **Instant virtual card issuance:** One-tap creation with no physical delivery, Card type: Single-use (one transaction, auto-destroy), Multi-use (reusable with set limits), Merchant-locked (tied to specific merchant), Subscription-dedicated (for recurring payments only), Card naming: Custom labels ("Netflix Card", "AliExpress Card", "Travel Card"), Currency selection: KES, USD, EUR, GBP per virtual card, Funding source: Linked debit card, PayMo wallet, bank account, prepaid balance
- **Virtual card dashboard:** All virtual cards in card-stack or grid view, Card status: Active, frozen, expired, used (single-use), destroyed, Per-card balance/limit display, Transaction count and total spend per card, Creation date and expiry date
- **Virtual card lifecycle:** Create → Fund → Use → Monitor → Freeze/Destroy, Auto-expiry configuration: 24 hours, 7 days, 30 days, custom, Post-expiry: Auto-refund unused balance to source, Destroy on demand with immediate invalidation

### Section 5.3.2 — Single-Use Virtual Cards
- **Purpose-built for security:** One transaction only, auto-destroyed after first authorization, Ideal for: One-time online purchases, Untrusted merchants, Free trial signups (prevent unwanted charges), High-risk transactions
- **Configuration:** Exact amount lock (card only valid for specified amount), Merchant pre-lock (optional: specify merchant name/MCC), Currency lock, Time window: Valid for 1 hour, 24 hours, or until used
- **Usage flow:** Create card → Copy card details → Use at checkout → Auto-destroy after authorization → Refund unused balance, Real-time notification: "Single-use card used at [Merchant] for KES X — card destroyed"
- **Security benefits:** Real PAN never exposed, If merchant is breached, card is already invalid, No recurring charge risk, Full traceability: Every single-use card linked to original merchant

### Section 5.3.3 — Merchant-Locked Virtual Cards
- **Dedicated merchant cards:** Create a virtual card locked to a specific merchant/MCC, Prevents card use elsewhere even if details are stolen, Ideal for: Subscription services (Netflix, Spotify, DSTV online), Regular online merchants (Amazon, Jumia, Alibaba), Employee vendor cards (locked to specific supplier)
- **Merchant locking options:** Exact merchant name match, MCC category lock (e.g., only "Digital Goods"), Domain lock (e.g., only *.netflix.com), Transaction amount range per merchant
- **Management:** View all merchant-locked cards with merchant logo, Edit limits without changing card number, Pause merchant (temporarily block) without destroying card, Switch merchant (reassign to new merchant), Destroy and recreate if merchant changes

### Section 5.3.4 — Subscription-Dedicated Virtual Cards
- **Subscription management cards:** One virtual card per subscription service, Prevents cross-subscription fraud, Easy cancellation: Destroy card = automatic subscription stop, Budget control: Set exact monthly limit per subscription
- **Subscription tracking:** Linked subscription name, monthly amount, next billing date, Billing history per subscription card, Failed payment alerts (subscription card declined), Subscription cost analytics: Total monthly subscriptions, annual cost, upcoming renewals
- **Smart features:** Auto-top-up from primary funding source when balance low, Auto-increase limit notification when subscription price changes, Duplicate subscription detection, Subscription cancellation assistant: Generate cancellation email template, One-click destroy to stop payments

---

## PAGE 5.4 — VIRTUAL CREDIT CARD CENTER

### Section 5.4.1 — Virtual Credit Card Application & Approval
- **Credit assessment:** Application form: Income, employment, existing credit, purpose, Credit bureau check: TransUnion, Metropol, Creditinfo integration, Alternative scoring: M-Pesa statement analysis, utility payment history, card usage patterns, Real-time decision: Instant approval, conditional approval, manual review, Rejection with reason and improvement path
- **Credit limit determination:** Initial limit based on credit score and income, Limit range: KES 10,000 – KES 5,000,000, Limit increase requests: Income proof upload, automatic review every 6 months, Credit utilization tracking with health recommendations, Temporary limit increase: For travel, large purchases, emergencies (24-hour to 30-day)
- **Virtual credit card issuance:** Instant digital card upon approval (no waiting for physical card), Card details displayed in app: PAN, expiry, CVV, Full card art with credit limit display, Virtual card ready for immediate online use, Optional physical card request for ATM/POS use

### Section 5.4.2 — Virtual Credit Card Controls
- **Spending controls:** Credit limit utilization alert at 50%, 80%, 95%, Per-transaction limit below overall credit limit, Daily/weekly/monthly spend caps, Cash advance toggle (if enabled, separate limit), Balance transfer toggle
- **Repayment controls:** Auto-repay: Full balance, minimum due, or custom amount on due date, Repayment source priority: PayMo wallet → M-Pesa → Bank account → Salary, Early repayment with interest savings calculator, Partial repayment scheduling
- **Interest & fee transparency:** Current APR display, Daily interest accrual tracker, Grace period countdown (typically 30-45 days), Late fee warning with exact amount and date, Total interest paid YTD, Interest savings from early repayment

### Section 5.4.3 — Credit Card Repayment & Billing
- **Bill generation & delivery:** Monthly statement generation on fixed date, Statement delivery: In-app, email, SMS summary, PDF download with full transaction details, Statement contents: Opening balance, transactions (purchases, payments, fees, interest), closing balance, minimum due, due date, credit available, reward points
- **Repayment methods:** Full balance payment (interest-free), Minimum payment (KES 2,000 or 5% of balance, whichever is higher), Custom amount payment, Scheduled auto-payment setup, One-tap payment from PayMo wallet or M-Pesa
- **Repayment tracking:** Payment due date countdown, Overdue alerts: 3 days before, on due date, 1 day after, 7 days after, Late fee application with breakdown, Credit score impact warning for late payments, Payment plan negotiation for distressed accounts

### Section 5.4.4 — Credit Card Rewards & Benefits
- **Rewards program:** Points earning: 1 point per KES 100 spent (configurable), Bonus categories: 2x/3x/5x points for dining, fuel, travel, online, Points balance and expiry tracking, Points redemption: Statement credit, M-Pesa transfer, airtime, merchant vouchers, travel bookings
- **Cashback program:** Percentage cashback per category, Monthly cashback cap, Cashback auto-credit to card or wallet, Cashback history and projection
- **Card benefits:** Travel insurance (when ticket purchased with card), Purchase protection (90-day damage/theft coverage), Extended warranty (double manufacturer warranty), Price protection (refund if price drops within 30 days), Lounge access (premium cards), Concierge service (premium cards)

---

## PAGE 5.5 — PREPAID CARD MANAGEMENT

### Section 5.5.1 — Prepaid Card Issuance & Types
- **Prepaid card types:** General purpose reloadable (GPR): For everyday spending, gift, travel, payroll, Gift card: Fixed amount, non-reloadable, customizable design, Travel card: Multi-currency, locked exchange rates, no FX fees, Teen/student card: Parent-controlled, spending limits, merchant blocks, Corporate expense card: Employee spending with real-time controls, Government disbursement card: Social protection, agricultural subsidy, emergency relief, Remittance card: Receive international remittances directly to card
- **Card creation:** Select type → Load initial amount → Set PIN → Card active, Instant virtual prepaid card + optional physical card, Card design selection per type, Card naming and labeling
- **Bulk prepaid issuance (corporate/government):** Upload beneficiary list (CSV: name, ID, phone, amount), Auto-KYC for known beneficiaries, Batch card creation and funding, Distribution: Digital delivery (virtual), physical mail, branch pickup, Activation tracking per card

### Section 5.5.2 — Prepaid Card Funding & Reload
- **Funding methods:** PayMo wallet transfer, M-Pesa direct load, Bank transfer (PesaLink/EFT/RTGS), Card-to-card transfer, Cash load at agent/branch, Salary direct deposit (payroll cards), Government disbursement direct load, International remittance direct load
- **Auto-reload rules:** Reload when balance falls below threshold, Scheduled reload (weekly, monthly), Percentage of salary auto-load, Round-up savings: Round purchases to nearest 100, save difference to prepaid
- **Funding limits:** Per-load minimum/maximum, Daily/weekly/monthly load limits, Card maximum balance cap, Source verification for large loads (KES 100,000+)

### Section 5.5.3 — Prepaid Card Spending & Controls
- **Spending rules:** Daily transaction limit, Per-transaction limit, Merchant category restrictions, Geographic restrictions, Online/offline toggle, ATM withdrawal toggle (if applicable), Cashback toggle
- **Balance management:** Real-time balance display, Low balance alerts at KES 500, 200, 100, Balance inquiry via app, SMS, USSD, ATM, Transaction history with filtering, Unused balance refund request (to source or M-Pesa)
- **Card expiry & renewal:** Expiry date tracking, Auto-renewal for reloadable cards, Balance transfer to new card before expiry, Non-reloadable card: Use by expiry or forfeit (per terms)

---

## PAGE 5.6 — CORPORATE & BUSINESS CARD PROGRAMS

### Section 5.6.1 — Corporate Card Program Setup
- **Program configuration:** Company profile: Name, KRA PIN, industry, size, Card program type: Employee expense cards, Department cards, Project cards, Virtual procurement cards, Card policy: Spending limits, allowed MCCs, geographic restrictions, approval workflows, Card branding: Company logo, colors, card design, BIN selection: Dedicated BIN for large programs or shared BIN
- **Employee card issuance:** Bulk employee upload (CSV: name, ID, department, designation, spending limit), Per-employee card configuration: Limit, MCC allowlist, geographic scope, Individual or department-level budgets, Card delivery: Direct to employee or centralized to HR, Activation: Employee self-activation with company code + OTP
- **Department/Project cards:** Shared cards for department heads, Project-specific cards with budget caps, Cost center allocation per transaction, Multi-cardholder access with individual PINs

### Section 5.6.2 — Corporate Card Controls & Policies
- **Spending policies:** Per-employee daily/weekly/monthly limits, Per-transaction limits, Category restrictions: Travel, meals, fuel, accommodation, office supplies, others, Merchant allowlist/blocklist, Time-based rules: Business hours only, weekend exceptions for travel, Geographic rules: Domestic only, regional, global, Receipt requirement: Mandatory for transactions >KES 5,000, auto-reminder
- **Approval workflows:** Pre-approval: Request before large transactions, Post-approval: Review and approve after transaction, Approval tiers: Manager → Finance → Director → CFO, Delegation rules during approver absence, Bulk approval for routine expenses
- **Real-time monitoring:** Live transaction feed for all corporate cards, Instant push notifications to cardholder and manager, Out-of-policy transaction alerts, Duplicate transaction detection, Unusual spending pattern alerts

### Section 5.6.3 — Expense Management & Reconciliation
- **Receipt capture:** In-app photo upload with OCR extraction, Email receipt forwarding to dedicated address, Automatic merchant matching with transaction, Missing receipt chase: Auto-reminder to cardholder, Grace period: 7 days to upload before flagging
- **Expense categorization:** Auto-categorization by MCC, Manual category override, Cost center allocation, Project code tagging, GL code mapping for accounting integration
- **Reconciliation tools:** Real-time expense report generation, Per-employee, per-department, per-project spend reports, Budget vs. actual tracking, Variance analysis with drill-down, Accounting system integration: QuickBooks, Sage, SAP, Xero, CSV/Excel export for finance team
- **Reimbursement handling:** Personal expense on corporate card: Flag and process reimbursement, Cash advance reconciliation, Per diem tracking and settlement

### Section 5.6.4 — Corporate Card Billing & Settlement
- **Billing models:** Individual liability: Employee pays bill, company reimburses, Corporate liability: Company pays all charges centrally, Mixed liability: Company pays business, employee pays personal
- **Centralized billing:** Single monthly statement for all corporate cards, Per-card, per-employee, per-department breakdown, Automatic GL code allocation, Payment from company bank account or PayMo business wallet
- **Settlement options:** Full monthly settlement, Partial settlement with rolling balance, Auto-debit from designated corporate account, Early settlement discount (if applicable)

---

## PAGE 5.7 — CARD SECURITY & FRAUD PREVENTION

### Section 5.7.1 — Real-Time Fraud Monitoring
- **Transaction scoring engine:** Real-time risk score (0-100) for every transaction, Risk factors: Amount, merchant, location, time, device, velocity, behavior pattern, Card-not-present (CNP) risk elevation, 3D Secure challenge for high-risk transactions, Step-up authentication: OTP, biometric, PIN for suspicious transactions
- **Fraud alert system:** Instant push/SMS/email for flagged transactions, One-tap "This was me" / "This was not me" response, Auto-block on "not me" with card freeze, Investigation workflow: Auto → manual review → resolution, Fraud case tracking with reference number and timeline
- **Behavioral analytics:** Baseline spending pattern per cardholder, Deviation detection: Unusual merchant, amount, location, time, Velocity checks: Multiple transactions in short time, Geolocation impossibility (transactions in Nairobi and Mombasa within 1 hour)

### Section 5.7.2 — 3D Secure & Authentication
- **3D Secure 2.0:** Enrollment status per card, Frictionless flow: Low-risk transactions pass without challenge, Challenge flow: OTP or biometric for high-risk, Merchant-initiated authentication for recurring payments, Biometric authentication: Fingerprint, face ID for app-based 3DS
- **Tokenization:** Network tokenization (Visa Token Service, Mastercard MDES), Device-specific tokens for mobile wallets, Merchant-specific tokens for recurring payments, Token lifecycle: Create, suspend, resume, delete, Token security: Token cannot be used outside intended device/merchant
- **Strong Customer Authentication (SCA):** Two-factor authentication for online transactions, Something you know (PIN), something you have (phone), something you are (biometric), Exemptions: Low-value, recurring, merchant-initiated, subscription renewals

### Section 5.7.3 — Card Data Protection
- **PAN masking:** Full PAN never displayed in plain text, Last 4 digits only for identification, Full PAN reveal: Biometric/PIN gate with session timeout, Copy PAN: Secure clipboard with auto-clear after 30 seconds
- **CVV protection:** CVV never stored after first entry, Dynamic CVV (if supported): Rotating CVV for virtual cards, CVV reveal: Tap-to-show with auto-hide after 10 seconds
- **Secure element & HCE:** Physical card: EMV chip with secure element, Virtual card: Host Card Emulation (HCE) with tokenized PAN, Encryption: AES-256 for data at rest, TLS 1.3 for data in transit, Key management: Hardware Security Module (HSM) for key storage

### Section 5.7.4 — Dispute & Chargeback Management
- **Dispute initiation:** Select transaction → dispute reason → upload evidence, Dispute reasons: Unauthorized transaction, goods not received, goods not as described, duplicate charge, incorrect amount, canceled recurring, Refund not processed
- **Dispute workflow:** Filed → Under Review → Evidence Requested → Submitted to Network → Resolved, Timeline tracking: Visa/Mastercard SLA (typically 45-90 days), Status updates at each stage, Partial or full chargeback outcome
- **Evidence management:** Transaction receipt, merchant communication, delivery proof, product photos, police report (for fraud), Evidence upload portal with file type validation, Auto-formatting for network submission
- **Chargeback analytics:** Chargeback rate per card, per merchant, per category, Reason code analysis, Win/loss rate tracking, Merchant blacklisting for repeat offenders

---

## PAGE 5.8 — CARD ANALYTICS & REPORTING

### Section 5.8.1 — Card Portfolio Analytics
- **Issuance analytics:** Cards issued by type, by month, by channel, Activation rate: Issued vs. activated, Time to activation average, Card replacement frequency and reasons, Card cancellation reasons analysis
- **Usage analytics:** Transaction volume and value by card type, Active card rate (% of issued cards with transactions in last 90 days), Average transactions per active card per month, Average ticket size per card type, Channel mix: POS, ATM, online, contactless, mobile wallet
- **Revenue analytics:** Interchange revenue per card type, Fee revenue: Annual fee, replacement fee, late fee, cash advance fee, FX revenue (spread on international transactions), Net revenue per card, Customer lifetime value per card product

### Section 5.8.2 — Spend Analytics & Insights
- **Consumer insights:** Top spending categories with trend, Seasonal spending patterns, Weekend vs. weekday spending, Online vs. offline ratio, Domestic vs. international spend ratio, Recurring payment identification and total, Subscription spend tracking
- **Merchant insights:** Merchant concentration: % of spend at top 10 merchants, Merchant loyalty: Repeat vs. new merchant ratio, Merchant category performance, Cross-sell opportunities: "You spend KES X on fuel — get a fuel cashback card"
- **Predictive analytics:** Next month spend forecast based on historical patterns, Credit limit increase recommendation engine, Prepaid reload prediction, Churn risk: Cards with declining usage, Upsell opportunity: Debit to credit, standard to premium

### Section 5.8.3 — Corporate Card Reporting
- **Program-level reports:** Total corporate spend, active cards, transactions, Per-department spend breakdown, Per-employee spend ranking, Policy violation report: Out-of-policy transactions, missing receipts, exceeded limits, Cost center allocation accuracy, Budget utilization per department/project
- **Compliance reports:** Tax-deductible expense summary, Per diem compliance audit, Mileage and fuel reconciliation, Entertainment and gift expense tracking, Regulatory reporting: CBK, KRA requirements
- **Custom reports:** Report builder: Drag-and-drop fields, filters, groupings, Scheduled reports: Daily, weekly, monthly auto-delivery, Export formats: PDF, Excel, CSV, API access for ERP integration

---

## PAGE 5.9 — CARD PROGRAM ADMINISTRATION (Issuer/BAAS Operator)

### Section 5.9.1 — BIN & Card Product Management
- **BIN management:** BIN allocation from card network (Visa/Mastercard), BIN configuration: Card type, currency, country, program type, BIN-level controls: Default limits, default MCC restrictions, BIN performance monitoring: Transaction volume, approval rate, fraud rate, BIN migration: Move card programs between BINs
- **Card product catalog:** Product definition: Name, type, target segment, features, fees, limits, Product lifecycle: Draft → Testing → Live → Deprecated → Retired, A/B testing: Test different fee structures, reward programs, Feature toggles per product: Enable/disable specific features, Product sunset: Migrate cardholders before retirement

### Section 5.9.2 — Card Production & Personalization
- **Personalization bureau integration:** EMV chip data preparation, Magnetic stripe encoding, Contactless antenna integration, Card art printing: Standard, custom photo, corporate branded, Quality control: Chip read test, magnetic stripe test, contactless test, Batch production tracking: Print date, personalization date, dispatch date
- **Inventory management:** Blank card stock tracking, Personalized card inventory (ready for activation), Rejected cards and destruction log, Reorder triggers based on issuance velocity

### Section 5.9.3 — Network & Processor Management
- **Network integration:** Visa/Mastercard certification and compliance, Network rule updates and implementation, Interchange fee schedule management, Chargeback rule compliance, Network reporting: Monthly volume reports, fraud reports
- **Processor management:** Transaction processor configuration, Authorization routing rules, Stand-in processing setup for outages, Settlement reconciliation: Processor vs. network vs. internal, Processor performance SLA monitoring

### Section 5.9.4 — Regulatory & Compliance Reporting
- **CBK reporting:** Card issuance statistics, Transaction volumes and values, Outstanding credit balances, Non-performing card loans, Fraud statistics, Chargeback ratios
- **KRA reporting:** Card fee revenue for tax, Withholding tax on interest (credit cards), VAT on card fees, Annual reporting templates
- **PCI DSS compliance:** Annual assessment and attestation, Quarterly vulnerability scans, Penetration testing, Access control and audit logs, Encryption key management compliance

---

## PAGE 5.10 — CARD SETTINGS & SUPPORT

### Section 5.10.1 — Card Preferences & Defaults
- **Default settings:** Default card for online payments, Default card for contactless, Default card for ATM withdrawals, Default funding source for virtual cards, Preferred currency for international transactions, Notification preferences: Push, SMS, email, WhatsApp per event type
- **Card naming & organization:** Custom nicknames for all cards, Card color coding, Card grouping: Personal, business, travel, subscriptions, Quick-access ordering: Drag to reorder cards in dashboard

### Section 5.10.2 — Notification & Alert Settings
- **Transaction alerts:** All transactions, transactions >KES X, international transactions only, declined transactions only, No alerts (not recommended)
- **Security alerts:** New device login, PIN change, card freeze/unfreeze, password change, suspicious activity, Card delivery status updates, Expiry reminders: 90 days, 60 days, 30 days, 7 days
- **Billing alerts:** Credit card statement ready, payment due reminder, payment received confirmation, minimum payment warning, late fee applied

### Section 5.10.3 — Card Support & Dispute Help
- **Self-service help:** FAQ by card type and issue, Troubleshooting wizard: "My card was declined" → reason diagnosis → solution, Card status checker, BIN lookup tool, Fee calculator
- **Support channels:** In-app chat with card support specialist, Phone hotline (dedicated card line), Email support with auto-ticket creation, WhatsApp Business support, Branch locator for in-person card support
- **Emergency services:** 24/7 lost/stolen hotline, Emergency card replacement (express courier), Emergency cash advance (for credit cardholders), Travel emergency assistance (premium cards)

---

**END OF DASHBOARD 5 OUTLINE**