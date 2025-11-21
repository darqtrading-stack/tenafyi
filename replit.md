# Tenafyi - Tenant Qualification at its Best

## Overview

Tenafyi is a full-stack web application designed for property managers to streamline tenant qualification and application processes. The system features a public tenant application form and an authenticated admin dashboard for managing applications, with advanced search and AI-powered query capabilities.

## System Architecture

### Frontend Architecture
- **React 18** with TypeScript for the user interface
- **Wouter** for client-side routing (lightweight alternative to React Router)
- **TailwindCSS** with **shadcn/ui** components for styling and UI elements
- **Vite** for build tooling and development server
- **TanStack Query** for server state management and caching

### Backend Architecture
- **Express.js** server with TypeScript
- **Replit Authentication** for secure admin access using OpenID Connect
- **PostgreSQL** database with **Drizzle ORM** for type-safe database operations
- **Neon Database** as the PostgreSQL provider
- RESTful API design with comprehensive error handling

### Database Design
The application uses PostgreSQL with the following key tables:
- `sessions` - Session management for Replit Auth (required)
- `users` - User profiles and authentication data (required)
- `applications` - Tenant application data with comprehensive fields
- `notes` - Admin notes attached to applications

## Key Components

### Authentication System
- **Replit Authentication**: Integrated OpenID Connect flow for admin access
- **Session Management**: PostgreSQL-backed session storage with connect-pg-simple
- **Authorization**: Route-level protection for admin endpoints

### Application Management
- **Public Application Form**: Multi-step form for tenant applications
- **Admin Dashboard**: Comprehensive interface for reviewing applications
- **Status Management**: Application lifecycle tracking (pending, approved, rejected, etc.)
- **Note System**: Admin collaboration through application notes

### Search and AI Features
- **Custom Search Service**: Pattern-based filtering and querying
- **AI Query Service**: OpenAI GPT-4o integration for natural language queries
- **Fallback Service**: Pattern matching when AI services are unavailable
- **Smart Queries**: Pre-defined common searches for quick access

### Email Integration
- **Nodemailer**: SMTP email service for notifications
- **Application Confirmations**: Automated emails to applicants
- **Viewing Reminders**: Scheduled notification system

## Data Flow

1. **Tenant Application**: Public users submit applications through the multi-step form
2. **Data Validation**: Zod schemas ensure data integrity at API boundaries
3. **Database Storage**: Drizzle ORM handles type-safe database operations
4. **Admin Review**: Authenticated admins access applications through the dashboard
5. **Status Updates**: Admins can update application status and add notes
6. **Email Notifications**: System sends automated confirmations and reminders

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: PostgreSQL database connectivity
- **drizzle-orm**: Type-safe database ORM
- **openid-client**: Replit authentication implementation
- **nodemailer**: Email service integration
- **openai**: AI query capabilities

### UI Dependencies
- **@radix-ui/***: Comprehensive UI component primitives
- **@tanstack/react-query**: Server state management
- **tailwindcss**: Utility-first CSS framework
- **lucide-react**: Icon library

## Deployment Strategy

### Development Environment
- **Replit**: Primary development platform with hot reloading
- **Vite Dev Server**: Frontend development with HMR
- **tsx**: TypeScript execution for server development

### Production Build
- **Vite Build**: Frontend assets compilation
- **esbuild**: Server bundling for production
- **Static Asset Serving**: Express serves built frontend files

### Environment Configuration
- **DATABASE_URL**: PostgreSQL connection string
- **SESSION_SECRET**: Session encryption key
- **OPENAI_API_KEY**: AI service authentication
- **SMTP_***: Email service configuration
- **REPLIT_DOMAINS**: Authentication domain configuration

## User Preferences

Preferred communication style: Simple, everyday language.

## Recent Changes

### November 18, 2025 - Universal Footer with Admin Login
- **Reusable Footer Component**: Created consistent footer (`Footer.tsx`) with copyright text and admin login link
- **Universal Navigation**: Footer appears on all pages (Landing, TenafyiLanding all views, AdminDashboard, ConversationalBot)
- **Clickable Logos**: All Tenafyi logos now navigate to home page with hover effects
- **Flex Layout System**: Implemented `min-h-screen flex flex-col` with `flex-1` main content to pin footer to bottom
- **Responsive Design**: Footer adapts to mobile and desktop viewports, always staying at page bottom
- **Admin Access**: Users can access admin login from any page via footer link
- **Consistent UX**: Unified navigation pattern across entire application

### November 18, 2025 - AI Tenant Chatbot System
- **AI Chatbot Integration**: OpenAI GPT-4o powered conversational assistant for tenant qualification
- **Admin Settings Panel**: Complete settings UI with feature toggles for AI bot, conversational bot, and traditional form
- **Letting Rules Engine**: Configurable income multiplier (rent × 30 default), self-employed profit validation, benefits acceptance
- **Income Calculations**: Real-time income qualification with guarantor suggestions when needed
- **Public Settings API**: Unauthenticated `/api/settings/public` endpoint for landing page feature toggles
- **Conditional UI**: Landing page dynamically shows 1-3 application methods based on admin configuration
- **Service Architecture**: 
  - `settingsService`: In-memory settings & letting rules storage
  - `rulesEngine`: Income calculations and qualification logic
  - `aiTenantService`: OpenAI integration with session management, rate limiting (50 messages/session)
- **Security Features**: API key handling via environment variables, input sanitization, abuse detection concepts
- **Database Resilience**: In-memory fallback for settings/rules when database is unavailable
- **AI Features**:
  - Natural language property Q&A
  - Smart income qualification guidance  
  - Real-time rent × multiplier calculations
  - Handles employed, self-employed, benefits income
  - Guarantor threshold suggestions (configurable percentage)
  - Conversation transcript storage for admin review

### September 1, 2025
- **System Validation Complete**: Comprehensive testing with 100 applicants (100% success rate)
- **Property Integration**: Live JT Property Consultants integration with 8 properties (£875-£3,495/month)
- **Schema Fixes**: Resolved annual income validation (string vs number type issues)
- **Question Alignment**: Bot and form now use unified questions structure for consistency
- **Visual Feedback**: Enhanced radio button styling with blue selection indicators and checkmarks
- **Form Auto-Reset**: Questionnaire now automatically starts from step 1 on new page visits
- **URL Verification**: Property scraping service working with fallback system for reliability
- **Database Status**: 180 total applications successfully processed and stored
- **Testing Coverage**: All 20 user scenarios validated (families, students, professionals, etc.)
- **Fresh Data System**: Property scraping always clears old data and fetches fresh listings
- **Scheduled Updates**: Automatic property refresh 3x daily (5am, 12pm, 6pm) with fresh data clearing
- **Manual Refresh**: Admin back office button for on-demand property updates with fresh data
- **System Health Monitor**: Daily automated health checks at 12am with fault reporting via email
- **Comprehensive Testing**: Automated daily application flow testing with test applicant submissions
- **Email Fault Reporting**: Configurable admin email for critical system alerts and health reports
- **Production Ready**: System fully tested and verified for live deployment

### System Features Status

**Search Functionality**
- **Backend Processing**: Fully operational with advanced fuzzy matching and complex logic
- **Advanced Features**: Handles spelling errors, informal language, AND/OR/NOT logic
- **Complex Queries**: "earning over £50k without dog who isn't self employed"
- **Misspelled Queries**: "wana move asap", "not smkers", "self emploied"  
- **Informal Language**: "any1 makin", "r students", "got guarantor"
- **Data Transmission**: Fixed API client to properly return JSON responses

**Tenafyi v3.2 Conversational Bot with Property Browser**
- **Chat Interface**: Complete messaging-style experience like WhatsApp/Messenger
- **Enhanced Flow**: 18+ step conversation with move-in date question and property browsing
- **Real Property Data**: Integration with live JT Property Consultants listings (8 properties £875-£3,495/month)
- **Property Browser Modal**: Full property details with "View Details" and "Select Property" functionality
- **Move-in Options**: Added "I need to give one months notice" to ASAP and "Within 2 weeks" options
- **Pet Details Collection**: Enhanced pet question with details input when user has pets
- **Enhanced Validation**: All required fields with 3-character minimums and comprehensive error handling
- **Fuzzy Matching**: Handles spelling errors, variations, and informal input across all questions
- **Real-time Responses**: Bot acknowledges each answer and guides to next question
- **Affordability Display**: Shows calculated rent affordability in conversation
- **Error Recovery**: Three-option system (Try Again, Start Over, Raise Ticket)
- **Email Integration**: Automatic support ticket creation with conversation context
- **Review Summary**: Chat-style confirmation before final submission
- **Mobile-First**: Optimized for conversational mobile experience

### Property Matching Enhancement
- **Live Property Integration**: Real properties from https://jtpropertyconsultants.co.uk/property-to-rent
- **Browse All Properties**: Modal interface with pricing, addresses, and external links
- **Advanced Fuzzy Matching**: Handles misspellings, abbreviations, and partial property names
- **Smart Confirmation Flow**: Single best match confirmation with "Did you mean?" prompt
- **Comprehensive Fallback**: Scrollable property list with "Browse All Properties" option
- **External Link Integration**: "View Details" buttons open full property pages in new tabs
- **Direct Selection**: "Select This Property" buttons continue application process seamlessly
- **Robust Error Handling**: Never freezes, handles empty input, always provides options
- **Exact Property Storage**: Stores selected property title and URL for application processing

## User Preferences

Preferred communication style: Simple, everyday language without technical jargon.

## Changelog

- June 24, 2025: PropertyCRM system built from scratch with comprehensive search capabilities