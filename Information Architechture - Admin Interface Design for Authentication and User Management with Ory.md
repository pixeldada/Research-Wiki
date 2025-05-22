# Admin Interface Design for Authentication and User Management with Ory

A comprehensive design for admin interface screens focused on authentication method setup and user import functionality using Ory.

## Authentication Method Setup Screens

### 1. Authentication Methods Dashboard

**Purpose**: Central hub for managing all authentication methods.

**UI Components**:

- **Authentication Methods Overview Card**
    - Status indicators showing which methods are active
    - Quick metrics (e.g., "2 of 5 methods enabled")
    - Health status indicators for each configured method
- **Method Cards** (for each authentication type):
    - Toggle switch for enabling/disabling
    - Status indicator (Configured/Not Configured/Error)
    - Quick edit button
    - Last modified timestamp
    - Primary configuration details summary
- **Add New Method Button**
    - Prominent "+Add Method" button
    - Dropdown for selecting method type when clicked

**Layout**:

```

┌─ Authentication Methods ─────────────────────────────────┐
│                                                          │
│  Active Methods: 2 of 5                 + Add Method ▼   │
│                                                          │
│  ┌─ Password Authentication ─┐  ┌─ Social Login ──────┐  │
│  │                           │  │                      │  │
│  │  Status: Enabled          │  │  Status: Enabled     │  │
│  │                           │  │                      │  │
│  │  • Password Policy: Strong│  │  • Google: Enabled   │  │
│  │  • MFA Required: Yes      │  │  • Microsoft: Enabled│  │
│  │  • Last Updated: 05/20/25 │  │  • GitHub: Disabled  │  │
│  │                           │  │                      │  │
│  │  [Configure]              │  │  [Configure]         │  │
│  └───────────────────────────┘  └──────────────────────┘  │
│                                                          │
│  ┌─ SAML ──────────────────┐  ┌─ OAuth/OIDC ──────────┐  │
│  │                         │  │                        │  │
│  │  Status: Disabled       │  │  Status: Disabled      │  │
│  │                         │  │                        │  │
│  │  • Not Configured       │  │  • Not Configured      │  │
│  │                         │  │                        │  │
│  │  [Configure]            │  │  [Configure]           │  │
│  └─────────────────────────┘  └────────────────────────┘  │
│                                                          │
└──────────────────────────────────────────────────────────┘

```

### 2. Password Authentication Configuration Screen

**Purpose**: Configure username/password authentication settings.

**UI Components**:

- **Basic Settings Section**:
    - Toggle to enable/disable
    - Username format options (email, username, both)
    - Username requirements (min length, allowed characters)
- **Password Policy Section**:
    - Minimum length slider/input (8-64 characters)
    - Complexity requirements checkboxes:
        - Require uppercase letters
        - Require lowercase letters
        - Require numbers
        - Require special characters
    - Password expiration settings
    - Password history settings (prevent reuse of previous X passwords)
- **Multi-Factor Authentication Section**:
    - Toggle for requiring MFA
    - Options for allowed MFA methods:
        - TOTP (Google Authenticator, etc.)
        - WebAuthn/FIDO2 (security keys, biometrics)
        - SMS/Email codes
- **Login Attempt Security**:
    - Max failed attempts before lockout
    - Lockout duration settings
    - IP-based rate limiting options

**Layout Example**:

```

┌─ Password Authentication Configuration ──────────────────┐
│                                                          │
│  Password Authentication: [ON/OFF]                       │
│                                                          │
│  ┌─ Identity Settings ─────────────────────────────────┐ │
│  │                                                      │ │
│  │  Username Type:                                      │ │
│  │  ○ Email Address Only                               │ │
│  │  ○ Username Only                                    │ │
│  │  ● Email Address or Username                        │ │
│  │                                                      │ │
│  └──────────────────────────────────────────────────────┘ │
│                                                          │
│  ┌─ Password Policy ──────────────────────────────────┐ │
│  │                                                      │ │
│  │  Minimum Length: [12] characters                     │ │
│  │  └───┴───┴───┴───┴───┴───┴───┴───┴───┘              │ │
│  │      8   12  16  20  24  28  32  36  40             │ │
│  │                                                      │ │
│  │  Complexity Requirements:                            │ │
│  │  [✓] Require uppercase letters                       │ │
│  │  [✓] Require lowercase letters                       │ │
│  │  [✓] Require numbers                                 │ │
│  │  [✓] Require special characters                      │ │
│  │                                                      │ │
│  │  Password Expiration:                                │ │
│  │  ○ Never                                             │ │
│  │  ● Every: [90] days                                  │ │
│  │                                                      │ │
│  └──────────────────────────────────────────────────────┘ │
│                                                          │
│  [Cancel]                               [Save Changes]   │
└──────────────────────────────────────────────────────────┘

```

### 3. SAML Configuration Screen

**Purpose**: Set up SAML integration with external identity providers.

**UI Components**:

- **SAML Status Section**:
    - Toggle to enable/disable
    - Current status indicator
- **Service Provider (SP) Details Section**:
    - Entity ID display (automatically generated)
    - ACS URL display (automatically generated)
    - SP metadata download button
- **Identity Provider (IdP) Configuration Section**:
    - Option to upload IdP metadata XML file
    - Manual configuration fields:
        - IdP Entity ID input
        - IdP SSO URL input
        - IdP certificate upload/paste area
- **Attribute Mapping Section**:
    - Mapping fields for user attributes (IdP attribute → Ory schema)
    - Common mappings (username, email, name, groups)
    - Add custom mapping button
- **Advanced Settings Section**:
    - Signature and encryption options
    - Authentication context settings
    - Session lifetime settings

**Layout Example**:

```

┌─ SAML Configuration ───────────────────────────────────┐
│                                                        │
│  SAML Authentication: [ON/OFF]                         │
│                                                        │
│  ┌─ Service Provider (SP) Information ─────────────┐   │
│  │                                                 │   │
│  │  These details will be provided to your IdP:    │   │
│  │                                                 │   │
│  │  Entity ID:                                     │   │
│  │  https://example.org/auth/saml/metadata         │   │
│  │                                        [Copy]   │   │
│  │                                                 │   │
│  │  ACS URL:                                       │   │
│  │  https://example.org/auth/saml/callback         │   │
│  │                                        [Copy]   │   │
│  │                                                 │   │
│  │  [Download SP Metadata XML]                     │   │
│  └─────────────────────────────────────────────────┘   │
│                                                        │
│  ┌─ Identity Provider (IdP) Configuration ──────────┐  │
│  │                                                  │  │
│  │  Upload IdP Metadata:                            │  │
│  │  [Choose File] No file chosen                    │  │
│  │                                    [Upload]      │  │
│  │                                                  │  │
│  │  - OR Configure Manually -                       │  │
│  │                                                  │  │
│  │  IdP Entity ID:                                  │  │
│  │  [                                          ]    │  │
│  │                                                  │  │
│  │  IdP Single Sign-On URL:                         │  │
│  │  [                                          ]    │  │
│  │                                                  │  │
│  │  IdP Certificate:                                │  │
│  │  [                                          ]    │  │
│  │  [                                          ]    │  │
│  │                                                  │  │
│  └──────────────────────────────────────────────────┘  │
│                                                        │
│  ┌─ Attribute Mapping ───────────────────────────────┐ │
│  │                                                   │ │
│  │  Map IdP attributes to user properties:           │ │
│  │                                                   │ │
│  │  Username:      [NameID]          ▼              │ │
│  │  Email:         [mail]            ▼              │ │
│  │  First Name:    [givenName]       ▼              │ │
│  │  Last Name:     [surname]         ▼              │ │
│  │  Groups:        [groups]          ▼              │ │
│  │                                                   │ │
│  │  [+ Add Custom Attribute Mapping]                 │ │
│  └───────────────────────────────────────────────────┘ │
│                                                        │
│  [Test Configuration]  [Cancel]  [Save Configuration]  │
└────────────────────────────────────────────────────────┘

```

### 4. OAuth 2.0 / OpenID Connect Configuration Screen

**Purpose**: Configure OAuth 2.0 and OpenID Connect provider integrations.

**UI Components**:

- **OAuth/OIDC Status Section**:
    - Toggle to enable/disable
    - Current status indicator
- **Provider Selection Section**:
    - Tabs or dropdown for different providers (Google, Microsoft, GitHub, etc.)
    - Custom provider option
- **Provider Configuration Section**:
    - Client ID input
    - Client Secret input
    - Authorized redirect URIs (auto-generated + custom)
    - Scopes selection (profile, email, etc.)
- **Advanced Settings Section**:
    - Token lifetime settings
    - Refresh token settings
    - PKCE settings

**Layout Example**:

```

┌─ OAuth 2.0 / OpenID Connect Configuration ──────────────┐
│                                                         │
│  OAuth/OIDC Authentication: [ON/OFF]                    │
│                                                         │
│  ┌─ Provider Selection ─────────────────────────────┐   │
│  │                                                  │   │
│  │  [Google] [Microsoft] [GitHub] [Facebook] [+Add] │   │
│  └──────────────────────────────────────────────────┘   │
│                                                         │
│  ┌─ Google Provider Configuration ────────────────────┐ │
│  │                                                    │ │
│  │  Client ID:                                        │ │
│  │  [                                           ]     │ │
│  │                                                    │ │
│  │  Client Secret:                                    │ │
│  │  [                                           ]     │ │
│  │                                                    │ │
│  │  Authorized Redirect URI:                          │ │
│  │  https://example.org/auth/google/callback          │ │
│  │                                         [Copy]     │ │
│  │                                                    │ │
│  │  Requested Scopes:                                 │ │
│  │  [✓] openid                                        │ │
│  │  [✓] profile                                       │ │
│  │  [✓] email                                         │ │
│  │  [ ] drive                                         │ │
│  │  [ ] calendar                                      │ │
│  │                                                    │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  ┌─ User Attribute Mapping ──────────────────────────┐  │
│  │                                                   │  │
│  │  Map provider claims to user properties:          │  │
│  │                                                   │  │
│  │  Username:     [email]            ▼              │  │
│  │  Email:        [email]            ▼              │  │
│  │  First Name:   [given_name]       ▼              │  │
│  │  Last Name:    [family_name]      ▼              │  │
│  │                                                   │  │
│  └───────────────────────────────────────────────────┘  │
│                                                         │
│  [Test Configuration]  [Cancel]  [Save Configuration]   │
└─────────────────────────────────────────────────────────┘

```

## User Import Screens

### 1. User Import Dashboard

**Purpose**: Central hub for all user import operations.

**UI Components**:

- **Import Methods Selection**:
    - Cards for different import methods (CSV, API, External IdP)
    - Quick start guides for each method
- **Recent Imports Table**:
    - List of recent import operations
    - Status indicators (Completed, Failed, In Progress)
    - Timestamps
    - User counts
    - Logs/details links

**Layout Example**:

```

┌─ User Import ────────────────────────────────────────────┐
│                                                          │
│  Select Import Method                                    │
│                                                          │
│  ┌─ CSV/Excel Import ─────┐  ┌─ API Import ────────────┐ │
│  │                        │  │                         │ │
│  │  Import users from     │  │  Import users           │ │
│  │  spreadsheet files     │  │  programmatically       │ │
│  │                        │  │                         │ │
│  │  [Start Import]        │  │  [View Documentation]   │ │
│  └────────────────────────┘  └─────────────────────────┘ │
│                                                          │
│  ┌─ External IdP Import ──┐  ┌─ Bulk User Creation ────┐ │
│  │                        │  │                         │ │
│  │  Import from Azure AD, │  │  Create multiple users  │ │
│  │  Google, or other IdPs │  │  manually               │ │
│  │                        │  │                         │ │
│  │  [Configure]           │  │  [Create Users]         │ │
│  └────────────────────────┘  └─────────────────────────┘ │
│                                                          │
│  Recent Import Operations                                │
│  ┌──────────────────────────────────────────────────────┐│
│  │ Date        | Method | Status    | Users | Details   ││
│  │─────────────────────────────────────────────────────-││
│  │ 05/21/25    | CSV    | Completed | 126   | [View]    ││
│  │ 05/18/25    | Azure  | Failed    | 0     | [View]    ││
│  │ 05/15/25    | CSV    | Completed | 83    | [View]    ││
│  └──────────────────────────────────────────────────────┘│
└──────────────────────────────────────────────────────────┘

```

### 2. CSV/Excel User Import Screen

**Purpose**: Import users from spreadsheet files with field mapping.

**UI Components**:

- **File Upload Section**:
    - File upload component with drag-and-drop
    - File format guidelines
    - Template download option
- **Preview Section**:
    - Table showing sample data from uploaded file
    - Column headers and first few rows
- **Field Mapping Section**:
    - Mapping controls for each column to Ory schema fields
    - Required fields indicators
    - Data validation feedback
- **Import Options Section**:
    - Password handling options (generate random, use from file, etc.)
    - Duplicate handling options (skip, update, error)
    - Email verification options
    - User activation settings

**Layout Example**:

```

┌─ CSV/Excel User Import ────────────────────────────────────┐
│                                                            │
│  Step 1: Upload File                                       │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                                                     │   │
│  │  Drag files here or [Choose File]                   │   │
│  │                                                     │   │
│  │  Supported formats: .csv, .xlsx, .xls               │   │
│  │                                                     │   │
│  │  [Download Template]                                │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                            │
│  Step 2: Preview Data                                      │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ Row | email          | first_name | last_name | ... │   │
│  │─────────────────────────────────────────────────────│   │
│  │ 1   | john@ex.com    | John       | Doe       | ... │   │
│  │ 2   | jane@ex.com    | Jane       | Smith     | ... │   │
│  │ 3   | mike@ex.com    | Mike       | Johnson   | ... │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                            │
│  Step 3: Map Fields                                        │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                                                     │   │
│  │  File Column      Ory Identity Field                │   │
│  │  ───────────      ────────────────                  │   │
│  │  email         →  traits.email         [Required] ▼ │   │
│  │  first_name    →  traits.name.first              ▼ │   │
│  │  last_name     →  traits.name.last               ▼ │   │
│  │  phone         →  traits.phone                    ▼ │   │
│  │  department    →  traits.department               ▼ │   │
│  │  password      →  credentials.password            ▼ │   │
│  │                                                     │   │
│  │  [+ Add Custom Mapping]                             │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                            │
│  Step 4: Import Options                                    │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                                                     │   │
│  │  Password Handling:                                 │   │
│  │  ○ Use passwords from file (if available)           │   │
│  │  ○ Generate random passwords                        │   │
│  │  ● Force password reset on first login              │   │
│  │                                                     │   │
│  │  Duplicate Handling:                                │   │
│  │  ○ Skip existing users                              │   │
│  │  ● Update existing users                            │   │
│  │  ○ Error on duplicates                              │   │
│  │                                                     │   │
│  │  [✓] Send welcome email to imported users           │   │
│  │  [✓] Require email verification                     │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                            │
│  [Cancel]  [Back]  [Validate Data]  [Start Import]         │
└────────────────────────────────────────────────────────────┘

```

### 3. External IdP User Import Screen

**Purpose**: Import users from external identity providers like Azure AD or Google Workspace.

**UI Components**:

- **Provider Selection Section**:
    - Dropdown or cards for selecting identity provider
    - Connection status indicator
- **Connection Configuration Section**:
    - Authentication settings for connecting to the provider
    - Test connection button
- **User Selection Section**:
    - Filters for selecting users to import (groups, departments, etc.)
    - Search functionality
    - Preview of users that will be imported
- **Attribute Mapping Section**:
    - Mapping controls for provider attributes to Ory schema
    - Advanced mapping options

**Layout Example**:

```

┌─ External IdP User Import ──────────────────────────────┐
│                                                         │
│  Step 1: Select Provider                                │
│  ┌────────────────────────────────────────────────────┐ │
│  │                                                    │ │
│  │  Provider: [Azure AD ▼]                            │ │
│  │                                                    │ │
│  │  Status: Not Connected                             │ │
│  │                                                    │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  Step 2: Configure Connection                           │
│  ┌────────────────────────────────────────────────────┐ │
│  │                                                    │ │
│  │  Tenant ID:                                        │ │
│  │  [                                          ]      │ │
│  │                                                    │ │
│  │  Client ID:                                        │ │
│  │  [                                          ]      │ │
│  │                                                    │ │
│  │  Client Secret:                                    │ │
│  │  [                                          ]      │ │
│  │                                                    │ │
│  │  [Test Connection]                                 │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  Step 3: Select Users                                   │
│  ┌────────────────────────────────────────────────────┐ │
│  │                                                    │ │
│  │  Filter by:                                        │ │
│  │  Groups: [All Groups ▼]                            │ │
│  │  Department: [All Departments ▼]                   │ │
│  │                                                    │ │
│  │  Search: [                              ]          │ │
│  │                                                    │ │
│  │  Preview (125 users will be imported):             │ │
│  │  ┌─────────────────────────────────────────────┐  │ │
│  │  │ Name           | Email            | Dept    │  │ │
│  │  │─────────────────────────────────────────────│  │ │
│  │  │ John Doe       | john@ex.com     | Sales   │  │ │
│  │  │ Jane Smith     | jane@ex.com     | IT      │  │ │
│  │  │ ...            | ...             | ...     │  │ │
│  │  └─────────────────────────────────────────────┘  │ │
│  │                                                    │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  Step 4: Map Attributes                                 │
│  ┌────────────────────────────────────────────────────┐ │
│  │                                                    │ │
│  │  Provider Attribute     Ory Identity Field         │ │
│  │  ─────────────────      ────────────────           │ │
│  │  userPrincipalName  →  traits.email         [▼]   │ │
│  │  givenName         →  traits.name.first     [▼]   │ │
│  │  surname           →  traits.name.last      [▼]   │ │
│  │  mobilePhone       →  traits.phone          [▼]   │ │
│  │  department        →  traits.department     [▼]   │ │
│  │                                                    │ │
│  │  [+ Add Custom Mapping]                            │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  Step 5: Import Options                                 │
│  ┌────────────────────────────────────────────────────┐ │
│  │                                                    │ │
│  │  [✓] Create SSO links for imported users           │ │
│  │  [✓] Force password reset for non-SSO login        │ │
│  │  [✓] Keep users in sync (periodic updates)         │ │
│  │  [ ] Replace existing users with same email        │ │
│  │                                                    │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  [Cancel]  [Back]  [Preview Import]  [Start Import]     │
└─────────────────────────────────────────────────────────┘

```

### 4. Import Results & Error Resolution Screen

**Purpose**: Review import operation results and resolve any errors.

**UI Components**:

- **Import Summary Section**:
    - Overall status
    - Success/failure counts
    - Timing information
- **Results Table**:
    - List of all users in the import batch
    - Status indicators for each user
    - Error messages for failed imports
- **Error Resolution Controls**:
    - Retry options for failed imports
    - Edit functionality for fixing data issues
    - Skip/ignore options

**Layout Example**:

```

┌─ Import Results ────────────────────────────────────────┐
│                                                         │
│  Import Summary                                         │
│  ┌────────────────────────────────────────────────────┐ │
│  │                                                    │ │
│  │  Status: Completed with Errors                     │ │
│  │  Total Users: 125                                  │ │
│  │  Successfully Imported: 118                        │ │
│  │  Failed: 7                                         │ │
│  │  Started: 05/22/25 10:15 AM                        │ │
│  │  Completed: 05/22/25 10:17 AM                      │ │
│  │                                                    │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  Results                                                │
│  ┌────────────────────────────────────────────────────┐ │
│  │ Filter: [All ▼]  Search: [                    ]    │ │
│  │                                                    │ │
│  │ User               | Status   | Error             │ │
│  │────────────────────────────────────────────────────│ │
│  │ john@ex.com        | Success  |                   │ │
│  │ jane@ex.com        | Success  |                   │ │
│  │ mike@ex.com        | Failed   | Invalid email     │ │
│  │ sarah@ex.com       | Failed   | Duplicate user    │ │
│  │ ...                | ...      | ...               │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  Error Resolution                                       │
│  ┌────────────────────────────────────────────────────┐ │
│  │                                                    │ │
│  │  [✓] Select All Failed Imports                     │ │
│  │                                                    │ │
│  │  Action for Selected:                              │ │
│  │  [Edit and Retry ▼]                                │ │
│  │                                                    │ │
│  │  [Apply]                                           │ │
│  │                                                    │ │
│  └────────────────────────────────────────────────────┘ │
│                                                         │
│  [Download Report]  [Back to Import]  [Done]            │
└─────────────────────────────────────────────────────────┘

```

## Implementation Details

### Ory API Integration

For each of these screens, you'll need to integrate with specific Ory APIs:

1. **Authentication Method Setup**:
    - For SAML: Configure Ory Hydra with SAML settings
    - For OAuth/OIDC: Use Ory Hydra's OAuth 2.0 and OIDC configuration endpoints
    - For password policies: Update Ory Kratos configuration
2. **User Import**:
    - Use Ory Kratos' admin APIs for identity creation:
        - `POST /admin/identities` for individual users
        - `PATCH /admin/identities` for batch operations
    - For password imports, utilize the hashed password format options

### Technical Considerations

1. **Form Validation**:
    - Client-side validation for immediate feedback
    - Server-side validation for security
    - Clear error messages with suggested fixes
2. **Progress Indicators**:
    - Loading spinners for asynchronous operations
    - Progress bars for batch operations
    - Status updates for long-running processes
3. **Error Handling**:
    - Detailed error messages from Ory APIs
    - User-friendly error explanations
    - Retry mechanisms for transient errors
4. **Security Considerations**:
    - CSRF protection for forms
    - Sensitive data handling (client secrets, passwords)
    - Proper permission checks for admin operations

## Design Best Practices

1. **Progressive Disclosure**:
    - Show basic options by default
    - Reveal advanced options when needed
    - Use expandable sections for complex configurations
2. **Clear Navigation**:
    - Breadcrumb trails for multi-step processes
    - Previous/Next buttons for wizards
    - Save/Cancel options at consistent locations
3. **Visual Hierarchy**:
    - Emphasize important actions and information
    - Group related controls
    - Use consistent spacing and alignment
4. **Feedback Mechanisms**:
    - Success/error toast notifications
    - Inline validation messages
    - Confirmation dialogs for destructive actions
5. **Accessibility**:
    - Proper ARIA labels
    - Keyboard navigation support
    - Sufficient color contrast