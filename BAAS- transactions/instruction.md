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

