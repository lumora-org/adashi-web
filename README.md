# Adashi Platform — Frontend

A mobile-first, multi-tenant Adashi management platform built to digitise traditional group savings and contribution systems in Nigeria.

The frontend provides an accessible and responsive interface for organisers, members, and platform administrators to create and manage Adashi groups, track contributions, monitor payout schedules, manage target-based savings, access financial records, and maintain transparency throughout each group round.

---

## 1. Project Overview

Adashi is designed to bring traditional group savings arrangements into a structured digital environment.

The platform supports two primary Adashi models:

### Rotational Adashi

Members contribute according to an agreed schedule. Each contribution cycle has a designated beneficiary who receives the contributions for that cycle. The beneficiary order is maintained throughout the group round.

Supported contribution schedules:

- Daily
- Weekly
- Every two weeks
- Every three weeks
- Monthly

### Target-Based Adashi

Members contribute towards a shared savings target. Once the group satisfies its distribution conditions, the accumulated funds are distributed equally among eligible members.

Members may contribute different amounts where group rules permit, but the confirmed distribution rule is equal distribution among eligible members.

---

## 2. Main Objectives

The frontend is responsible for:

- Providing a simple and intuitive experience for Nigerian users.
- Allowing users to create and manage multiple Adashi groups.
- Supporting users who act as organisers in some groups and members in others.
- Displaying contribution schedules and financial activity clearly.
- Providing transparent contribution and payout histories.
- Supporting secure payout confirmation and dispute reporting.
- Providing downloadable transaction receipts.
- Giving organisers useful financial and operational reports.
- Providing platform administrators with a dedicated administration portal.
- Supporting mobile, tablet, and desktop experiences.

---

## 3. Technology Stack

The frontend is expected to use the following technologies:

| Technology | Purpose |
|---|---|
| Next.js | React framework and application routing |
| TypeScript | Type safety |
| Tailwind CSS | Styling and responsive layouts |
| shadcn/ui | Reusable interface components |
| TanStack Query | Server state and API data management |
| React Hook Form | Form management |
| Zod | Form and data validation |
| PWA support | Installable mobile-friendly experience |
| Lucide React | Interface icons |

Use the package versions already established in the repository where possible. Avoid unnecessary dependency upgrades.

---

## 4. User Types and Access

The platform does not treat organiser and member as mutually exclusive global user roles.

A single registered user can:
- Create and organise multiple groups.
- Join multiple groups created by other users.
- Be an organiser in one group and a member in another.
- Access different features depending on their relationship with each group.

### Group organiser

The organiser can:
- Create and configure groups.
- Select an Adashi type.
- Configure contribution schedules and group rules.
- Invite and manage members.
- Manage group rounds.
- Record and verify reported contributions.
- Manage beneficiary order and payout schedules.
- Mark payouts as sent.
- Confirm payouts on behalf of members after the 48-hour deadline.
- Review withdrawal requests.
- View financial reports and group activity.

### Group member

A member can:
- Join groups through invitations.
- View group information and rules.
- View contribution schedules.
- Report payments.
- Upload payment evidence where applicable.
- View personal contribution summaries.
- View payout history and expected payouts.
- Confirm receipt of a payout.
- Dispute a payout.
- Submit withdrawal requests.
- Download authorised receipts.

### Platform administrators

The platform administration portal supports the following proposed platform-level roles:

- `SUPER_ADMIN`
- `PLATFORM_ADMIN`
- `PLATFORM_SUPPORT`
- `PLATFORM_FINANCE`
- `PLATFORM_AUDITOR`

Access must be controlled by permissions. Platform administrators must not automatically receive unrestricted access to financial operations.

---

## 5. Core Frontend Modules

### 5.1 Public Website

The public website introduces Adashi and explains its value.

Expected pages include:

- Home
- About
- How It Works
- Features
- Pricing
- Frequently Asked Questions
- Contact
- Sign In
- Create Account
- Privacy Policy
- Terms and Conditions

The landing page should communicate the benefits of transparent group savings, organised contributions, reliable payout tracking, and accessible financial records.

### 5.2 Authentication

Features include:

- User registration
- Login
- Logout
- Forgot password
- Password reset
- Session management
- Profile management

Authentication should use secure server-managed cookies where supported by the backend architecture.

Do not store long-lived authentication or refresh tokens in local storage.

### 5.3 User Dashboard

The dashboard should provide an overview of the user's activity.

Suggested information:

- Total active groups
- Groups organised
- Groups joined
- Pending contributions
- Verified contributions
- Upcoming contribution deadlines
- Expected payouts
- Recent financial activity
- Notifications
- Group invitations

Dashboard information should be based on authenticated API responses.

### 5.4 Group Management

Users should be able to:

- Create a group.
- Edit permitted group details.
- View group information.
- Invite members.
- Accept or decline invitations.
- View members and their membership status.
- Configure group rules.
- View group financial summaries.
- Suspend or close a group where authorised.

Each group must have a persistent identity.

A group can have multiple operational rounds over time. Completed rounds must remain accessible as historical records.

### 5.5 Group Rounds

A group round represents one operational savings cycle.

The frontend should support:

- Round creation.
- Round configuration.
- Round activation.
- Round progress tracking.
- Round financial summaries.
- Round completion.
- Historical round viewing.

Starting a new round requires a valid group activation entitlement or a successful group purchase.

A completed round should be read-only for ordinary users.

### 5.6 Billing and Entitlements

The platform uses a one-time group-round purchase model.

Proposed pricing:

| Plan | Maximum members | Price |
|---|---:|---:|
| Starter | 10 | ₦1,000 |
| Standard | 20 | ₦2,000 |
| Premium | 50 | ₦3,500 |
| Enterprise | Custom | Contact platform team |

Every user receives one free Starter group activation, subject to the platform's one-time eligibility rule.

Important frontend behaviour:

- Clearly display free entitlement availability.
- Clearly distinguish free activation from paid purchases.
- Show plan limits.
- Allow organisers to upgrade when member count exceeds their current plan.
- Display the upgrade price difference returned by the backend.
- Show payment status.
- Do not activate a paid group round based only on a frontend payment-success message.
- Refresh entitlement and round status from the backend after payment verification.

The backend is the final authority for entitlement eligibility, billing amounts, and activation.

### 5.7 Contribution Management

Members should be able to:

- View expected contributions.
- Report a payment.
- Enter the amount paid.
- Provide transaction references.
- Upload payment evidence.
- View verification status.
- View rejected or reversed contributions.

Organisers should be able to:

- Review reported contributions.
- Verify payments.
- Reject invalid payment reports with reasons.
- View outstanding contributions.
- Review contribution histories.

Contribution statuses include:

- `EXPECTED`
- `REPORTED`
- `VERIFIED`
- `REJECTED`
- `OVERDUE`
- `REVERSED`

Reporting a payment does not mean the payment has been verified.

### 5.8 Collection Methods

Each group selects one contribution collection method:

**Organiser collection**

Members transfer contributions to the organiser's designated bank account. The organiser records and verifies the payments.

**Direct beneficiary collection**

Members transfer contributions directly to the current beneficiary. The organiser records and verifies the payments.

The frontend must clearly display the selected collection method and relevant payment instructions.

### 5.9 Rotational Adashi

The rotational module should display:

- Contribution schedule.
- Current cycle.
- Current beneficiary.
- Beneficiary order.
- Expected contribution per member.
- Verified contributions.
- Outstanding contributions.
- Cycle progress.
- Payout status.
- Previous cycles.
- Upcoming cycles.

Organisers should be able to manage permitted schedule and beneficiary-order operations, subject to backend rules and audit requirements.

### 5.10 Target-Based Adashi

The target-based module should display:

- Group savings target.
- Total verified contributions.
- Progress towards target.
- Remaining target amount.
- Eligible members.
- Distribution status.
- Individual distribution amounts.
- Distribution history.

The frontend must not independently calculate authoritative distribution amounts. It should display the values calculated and returned by the backend.

### 5.11 Payout Management

The payout interface must support the following states:

- `PENDING`
- `SENT`
- `CONFIRMED_BY_MEMBER`
- `CONFIRMED_BY_ORGANISER`
- `DISPUTED`
- `CANCELLED`

Organiser workflow:

1. View a pending payout.
2. Mark the payout as sent.
3. Provide required transfer details or reference.
4. View the confirmation deadline.
5. Receive notification if the member has not confirmed after 48 hours.
6. Confirm on behalf of the member after the deadline, with a mandatory reason.

Member workflow:

1. Receive a payout notification.
2. View payout details.
3. Confirm receipt using the confirmation action.
4. Dispute the payout if the funds were not received.

**48-hour confirmation rule**

- The deadline is calculated from the backend's `sentAt` timestamp.
- The member has 48 elapsed hours to confirm.
- The frontend countdown is informational only.
- The frontend must never enable organiser confirmation before the backend deadline.
- Organiser confirmation must be clearly identified as an organiser action, not a member confirmation.
- Members must be able to dispute a payout even after organiser confirmation, subject to the backend's dispute rules.

### 5.12 Receipts

Every payout marked as sent automatically generates a receipt record.

The frontend should support:

- Receipt listing.
- Receipt details.
- Receipt status.
- PDF download.
- Receipt access for authorised organisers and beneficiaries.

Receipt generation states:

- `GENERATING`
- `AVAILABLE`
- `FAILED`
- `SUPERSEDED`

A receipt must distinguish whether the payout was confirmed by the member or confirmed by the organiser.

A receipt indicates that the platform recorded the payout as sent. It must not be presented as independent proof of bank settlement.

### 5.13 Withdrawals and Refunds

Members should be able to:

- Submit a withdrawal request.
- Provide a reason.
- View request status.
- View settlement calculations.
- View approved refunds and payment history.

Organisers should be able to:

- Review withdrawal requests.
- Approve or reject requests.
- View calculated settlements.
- Record refunds.
- Review the effect of withdrawal on beneficiary order and group financial position.

The frontend must display backend-calculated settlement amounts. It must not independently assume that a withdrawing member receives all contributions back.

### 5.14 Notifications

Notifications should cover:

- Group invitations.
- New group membership.
- Contribution reminders.
- Contribution verification or rejection.
- Upcoming payout.
- Payout marked as sent.
- Payout confirmation.
- Payout dispute.
- 48-hour confirmation deadline.
- Organiser confirmation on behalf.
- Withdrawal updates.
- Refund updates.
- Round completion.
- Billing and entitlement events.

Support in-app notifications, with email or other channels added according to backend capabilities.

### 5.15 Reports and Financial Summaries

Organisers should have access to:

- Total verified contributions.
- Total outstanding contributions.
- Contributions by member.
- Contributions by cycle.
- Total payouts.
- Remaining payout obligations.
- Refunds and withdrawals.
- Group financial position.
- Round financial history.

Members should see their own financial summary:

- Total verified contributions.
- Number of verified contributions.
- Pending contributions.
- Rejected contributions.
- Outstanding contributions.
- Amount received.
- Expected payout, where applicable.
- Contribution and payout history.

Financial totals must come from backend calculations based on transaction records.

### 5.16 Super Admin Portal

The administration portal should provide:

- Platform overview.
- User management.
- Group management.
- Round management.
- Plan and pricing management.
- Group purchase verification.
- Entitlement management.
- Platform revenue reports.
- Financial oversight.
- Dispute monitoring.
- Administrator management.
- Role and permission management.
- Platform settings.
- Audit log access.

Super Admin accounts must not be created through public registration.

---

## 6. Suggested Frontend Structure

The following is a recommended feature-based structure. Adapt it to the existing repository rather than replacing an established working architecture without reason.

```text
frontend/
├── public/
│   ├── icons/
│   ├── images/
│   └── manifest.json
│
├── src/
│   ├── app/
│   │   ├── (public)/
│   │   │   ├── page.tsx
│   │   │   ├── about/
│   │   │   ├── pricing/
│   │   │   └── how-it-works/
│   │   │
│   │   ├── (auth)/
│   │   │   ├── login/
│   │   │   ├── register/
│   │   │   └── forgot-password/
│   │   │
│   │   ├── dashboard/
│   │   ├── groups/
│   │   ├── rounds/
│   │   ├── contributions/
│   │   ├── payouts/
│   │   ├── receipts/
│   │   ├── withdrawals/
│   │   ├── notifications/
│   │   ├── reports/
│   │   └── admin/
│   │
│   ├── components/
│   │   ├── ui/
│   │   ├── layout/
│   │   ├── forms/
│   │   └── shared/
│   │
│   ├── features/
│   │   ├── auth/
│   │   ├── users/
│   │   ├── groups/
│   │   ├── memberships/
│   │   ├── rounds/
│   │   ├── billing/
│   │   ├── contributions/
│   │   ├── cycles/
│   │   ├── payouts/
│   │   ├── receipts/
│   │   ├── target-savings/
│   │   ├── withdrawals/
│   │   ├── notifications/
│   │   ├── reports/
│   │   └── administration/
│   │
│   ├── hooks/
│   ├── lib/
│   │   ├── api/
│   │   ├── auth/
│   │   ├── formatting/
│   │   └── validation/
│   │
│   ├── providers/
│   ├── types/
│   └── styles/
│
├── docs/
├── .env.example
├── next.config.ts
├── package.json
└── README.md
```

---

## 7. Environment Variables

Create a local `.env.local` file based on `.env.example`.

Example:

```env
NEXT_PUBLIC_APP_NAME=Adashi
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:4000/api/v1
```

Only expose variables prefixed with `NEXT_PUBLIC_` when they are genuinely safe for the browser.

Never put API secrets, database credentials, payment secrets, private storage credentials, or JWT secrets in frontend environment variables.

---

## 8. Local Development

### Requirements

- Node.js LTS compatible with the project's Next.js version.
- npm, pnpm, or the package manager already used by the repository.
- Running backend API.
- Environment variables configured.

### Installation

```bash
git clone <frontend-repository-url>
cd <frontend-project-folder>
npm install
```

### Configure environment

```bash
cp .env.example .env.local
```

Update the API URL and other required public configuration.

### Start development server

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

### Production build

```bash
npm run build
```

### Start production server

```bash
npm run start
```

### Lint

```bash
npm run lint
```

Use the actual scripts defined in `package.json` if they differ from these examples.

---

## 9. UI/UX Guidelines

The application should be mobile-first.

### Suggested colour palette

| Colour | Hex | Usage |
|---|---|---|
| Emerald | `#087F5B` | Primary actions and positive financial indicators |
| Navy | `#142B3B` | Navigation, headings and strong contrast |
| Gold | `#E7B54A` | Highlights and selected accents |
| Off-white | `#F6F8F7` | Main application background |
| White | `#FFFFFF` | Cards and content surfaces |

### Design principles

- Keep navigation simple.
- Make financial information easy to understand.
- Use clear status labels and badges.
- Use confirmation dialogs for important financial actions.
- Display loading, empty, success, and error states.
- Avoid overcrowded dashboards.
- Use accessible forms and keyboard navigation.
- Ensure buttons and tables work well on mobile devices.
- Format currency consistently in Nigerian Naira.
- Display dates and times clearly.
- Avoid relying on colour alone to communicate financial status.

### Currency formatting

Display currency in NGN using a consistent format, for example:

```text
₦1,500.00
₦25,000.00
₦1,250,000.00
```

Do not use frontend floating-point calculations for authoritative financial totals.

---

## 10. Security and Data Integrity

The frontend must:

- Enforce route-level access checks for user experience, while relying on the backend for actual authorisation.
- Never assume that hiding a button protects an API endpoint.
- Validate forms before submission.
- Display backend validation errors.
- Prevent duplicate submissions where possible.
- Use idempotency keys for supported financial operations.
- Avoid exposing private payment evidence or receipt files publicly.
- Never fabricate successful payments or payout confirmations.
- Never modify financial records directly from client-side state.
- Respect group-level permissions.

The backend remains the source of truth for financial balances, contribution verification, payout status, distribution amounts, billing, and entitlements.

---

## 11. Testing

The frontend should include tests for:

- Authentication and session handling.
- Group creation and invitations.
- Group round activation.
- Free Starter entitlement display.
- Plan selection and upgrade display.
- Contribution reporting.
- Contribution verification views.
- Rotational schedules.
- Target savings progress.
- Payout confirmation.
- 48-hour organiser override restrictions.
- Payout disputes.
- Receipt access and downloads.
- Withdrawal and refund workflows.
- Group-specific permissions.
- Super Admin access restrictions.
- Responsive layouts and accessibility.

Test important financial workflows against backend API responses rather than relying only on mocked UI states.

---

## 12. Deployment

The frontend can be deployed on Vercel or another compatible hosting provider.

Before deployment:

1. Configure production environment variables.
2. Set the production API URL.
3. Configure the production domain.
4. Verify CORS and cookie settings with the backend.
5. Confirm authentication works over HTTPS.
6. Test file upload and receipt downloads.
7. Verify PWA configuration.
8. Run a production build.
9. Test critical workflows in the production environment.

---

## 13. Documentation

The `docs/` directory contains the detailed product and engineering specifications.

Review the documentation before making significant changes. The README is an overview; the detailed specifications define the expected business rules, architecture, database design, API contracts, security requirements, and implementation tasks.

---

## 14. Contribution Guidelines

When contributing:

- Follow the existing project architecture.
- Use TypeScript types instead of unnecessary `any`.
- Reuse shared UI components.
- Keep feature logic organised.
- Avoid duplicating API logic.
- Validate user input.
- Handle loading and error states.
- Write tests for important workflows.
- Do not introduce frontend-only financial business rules.
- Update documentation when behaviour or API contracts change.

---

## 15. Important Product Rules

1. One account can organise multiple groups and join multiple groups.
2. Organiser and member permissions are group-specific.
3. A group persists across multiple operational rounds.
4. Every new group round requires an eligible free entitlement or paid activation.
5. Each user receives only one free Starter activation.
6. Contributions are separate from payouts.
7. Reported payments are not automatically verified.
8. Target-based distributions are equal among eligible members.
9. Members have 48 hours from payout `sentAt` to confirm receipt.
10. Organisers can confirm on behalf only after the deadline and must provide a reason.
11. Members can dispute payouts.
12. Every payout marked as sent creates a receipt record.
13. Financial records must remain traceable.
14. The platform does not hold group funds in an internal wallet in the MVP.

---

## 16. Project Status

This repository contains the frontend implementation of the Adashi platform. Features should be considered complete only when implemented, integrated with the backend, tested, and consistent with the approved project documentation.

**Adashi — Bringing transparency, structure, and trust to group savings.**
