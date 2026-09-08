# Reference
## Auth
<details><summary><code>client.auth.issueAccessToken(request) -> AccessTokenResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Issues a short-lived access token from the authenticated API key. Access tokens can optionally be bound to a specific employer or employee for scoped access. Tokens expire after 15 minutes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.auth().issueAccessToken(
    IssueAccessTokenRequest
        .builder()
        .grantType(GrantType.CLIENT_CREDENTIALS)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**grantType:** `GrantType` 

Token issuance flow. Currently only 'client_credentials' supported.

* `client_credentials` - client_credentials
    
</dd>
</dl>

<dl>
<dd>

**boundEntity:** `Optional<BoundEntity>` — Optional entity to bind the token to for scoped access
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Employees
<details><summary><code>client.employees.get(employeeId) -> EmployeeResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves detailed information for a specific employee by ID. Returns employee details including personal information, employment status, classification and compensation-type effective dates, compensation type, and payroll deductions from the most recent statement period. Deductions reflect a snapshot of the current period and are replaced when a new statement is generated.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employees().get(
    "empl_abc123def456",
    GetEmployeesRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employeeId:** `String` — Unique employee identifier (empl_*)
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employees.update(employeeId, request) -> EmployeeResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates employee personal, contact, address, and employment fields. This endpoint currently supports email, phone, gender, address, employee_class, start_date, and compensation_type. effective_date is required and applies to employee_class and compensation_type when those fields are included in the request.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employees().update(
    "empl_abc123def456",
    PatchedUpdateEmployeeRequest
        .builder()
        .effectiveDate("2023-03-01")
        .employeeClass(EmployeeClass.FULL_TIME)
        .startDate("2023-01-15")
        .compensationType(CompensationType.SALARY)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employeeId:** `String` — Unique employee identifier (empl_*)
    
</dd>
</dl>

<dl>
<dd>

**email:** `Optional<String>` — Email address
    
</dd>
</dl>

<dl>
<dd>

**phone:** `Optional<String>` — Phone number
    
</dd>
</dl>

<dl>
<dd>

**gender:** `Optional<Gender>` 

Gender identity

* `Male` - Male
* `Female` - Female
* `Transgender` - Transgender
* `Non-binary` - Non-binary
* `Prefer not to respond` - Prefer not to respond
    
</dd>
</dl>

<dl>
<dd>

**address:** `Optional<EmployeeAddressInput>` — Employee's residential address
    
</dd>
</dl>

<dl>
<dd>

**employeeClass:** `Optional<EmployeeClass>` 

Employment classification

* `Full Time` - Full Time
* `Part Time` - Part Time
* `Temporary` - Temporary
* `Intern` - Intern
* `Seasonal` - Seasonal
* `Individual Contractor` - Individual Contractor
    
</dd>
</dl>

<dl>
<dd>

**startDate:** `Optional<String>` — Employment start date
    
</dd>
</dl>

<dl>
<dd>

**compensationType:** `Optional<CompensationType>` 

Employee compensation type

* `Salary` - Salary
* `Hourly` - Hourly
    
</dd>
</dl>

<dl>
<dd>

**effectiveDate:** `String` — Past or present date applied to each tracked employment field included in this request
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employees.listEnrollments(employeeId) -> SyncPagingIterable&amp;lt;Enrollment&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a paginated list of benefit enrollments for an employee.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employees().listEnrollments(
    "empl_abc123def456",
    ListEnrollmentsEmployeesRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employeeId:** `String` — Unique employee identifier (empl_*)
    
</dd>
</dl>

<dl>
<dd>

**limit:** `Optional<Integer>` — Items per page (default: 20, max: 100)
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number (default: 1)
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Employers
<details><summary><code>client.employers.list() -> SyncPagingIterable&amp;lt;OrganizationEmployer&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the caller's employer book — every employer with its computed columns (enrollment-rate summary, benefit-family tags, HRIS connection, benefit-lifecycle stage) merged with the employer's flat CRM fields (legal name, EIN, contact, address, timestamps). The book is derived from the authenticated principal: one organization's employers, or every organization's for a caller whose reach is not a single organization. Supports search by display name, legal name, or exact EIN, employer id or contact email, benefit-family/lifecycle/HRIS filters, and page/limit pagination.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().list(
    ListEmployersRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**benefitFamily:** `Optional<BenefitFamilyParamItem>` — Filter to employers with at least one active benefit in these families.
    
</dd>
</dl>

<dl>
<dd>

**benefitLifecycleStage:** `Optional<BenefitLifecycleStageItem>` — Filter to employers in one of these computed benefit-lifecycle stages.
    
</dd>
</dl>

<dl>
<dd>

**hrisProvider:** `Optional<String>` — Filter to employers whose HRIS connection is with one of these payroll providers (e.g. `ADP RUN`). Matched case-insensitively; free text, so read the available values from the HRIS-providers endpoint rather than assuming a fixed set.
    
</dd>
</dl>

<dl>
<dd>

**hrisStatus:** `Optional<HrisStatusItem>` — Filter to employers whose HRIS connection is in one of these statuses.
    
</dd>
</dl>

<dl>
<dd>

**includeCancelled:** `Optional<Boolean>` — Include cancelled employers (hidden by default unless their stage is explicitly requested).
    
</dd>
</dl>

<dl>
<dd>

**limit:** `Optional<Integer>` — Items per page.
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number.
    
</dd>
</dl>

<dl>
<dd>

**search:** `Optional<String>` — Employer filter. Matches the display name or the legal name case-insensitively as a substring, or one of these exactly: the EIN (with or without its dash), the employer id, or the contact email of one of the employer's non-disabled admins.
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.create(request) -> EmployerResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new employer for the authenticated organization. Requires employer name, legal name, EIN, email, and address information. Returns the created employer with its assigned ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().create(
    CreateEmployerRequest
        .builder()
        .name("NewCo Industries")
        .legalName("NewCo Industries LLC")
        .ein("12-3456789")
        .email("hr@newco.com")
        .address(
            EmployerAddressInput
                .builder()
                .addressLine1("789 Business Blvd")
                .city("Seattle")
                .state("WA")
                .zipcode("98101")
                .addressLine2("Floor 5")
                .build()
        )
        .phoneNumber("2065550100")
        .referenceId("partner-emp-001")
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `String` — Employer display name
    
</dd>
</dl>

<dl>
<dd>

**legalName:** `String` — Legal business name
    
</dd>
</dl>

<dl>
<dd>

**ein:** `String` — Employer Identification Number (format: XX-XXXXXXX)
    
</dd>
</dl>

<dl>
<dd>

**email:** `String` — Email address for billing and communications
    
</dd>
</dl>

<dl>
<dd>

**address:** `EmployerAddressInput` — Employer address
    
</dd>
</dl>

<dl>
<dd>

**phoneNumber:** `Optional<String>` — Employer phone number (10-digit US format, e.g. 5551234567)
    
</dd>
</dl>

<dl>
<dd>

**referenceId:** `Optional<String>` — External reference ID for this employer
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.get(employerId) -> EmployerResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves detailed information for a specific employer by ID. The employer must belong to the authenticated organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().get(
    "empr_abc123def456",
    GetEmployersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.update(employerId, request) -> EmployerResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an existing employer. All fields are optional — only provided fields are updated. PO Box addresses are rejected.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().update(
    "empr_abc123def456",
    UpdateEmployerRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>

<dl>
<dd>

**name:** `Optional<String>` — Employer display name
    
</dd>
</dl>

<dl>
<dd>

**legalName:** `Optional<String>` — Legal business name
    
</dd>
</dl>

<dl>
<dd>

**address:** `Optional<UpdateEmployerAddressInput>` — Employer address
    
</dd>
</dl>

<dl>
<dd>

**active:** `Optional<Boolean>` — Whether the employer is active
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.listBenefitPlanYears(employerId) -> EmployerBenefitPlanYearsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the employer's benefit plan years (all years, or one when `year` is given), each with its benefits, offered states, benefit families, and the year-level enrollment roll-up. The caller must be authorized for the employer; an unknown or unauthorized employer returns 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().listBenefitPlanYears(
    "empr_abc123def456",
    ListBenefitPlanYearsEmployersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.getBenefitPlanYear(employerId, benefitPlanYearId) -> EmployerBenefitPlanYearResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one benefit plan year in full — its benefit details plus the per-benefit enrollment rate and SPD link — addressed by its `benefit_plan_year_id`. The caller must be authorized for the employer; an unknown or unauthorized plan year returns 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().getBenefitPlanYear(
    "empr_abc123def456",
    "plyr_abc123def456",
    GetBenefitPlanYearEmployersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**benefitPlanYearId:** `String` — Unique benefit-plan-year identifier (plyr_*).
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.listBenefitPlanYearEnrollments(employerId, benefitPlanYearId) -> SyncPagingIterable&amp;lt;PlanYearEnrollment&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of every member with an enrollment in one of an employer's plan years, any election status: what they elected, where their coverage stands, dependent count, carrier, plan, tier, and the plan's total monthly cost. The caller must be authorized for the employer `empr_<...>`; an unknown or unauthorized employer, or an unknown plan year `plyr_<...>`, returns 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().listBenefitPlanYearEnrollments(
    "empr_abc123def456",
    "plyr_abc123def456",
    ListBenefitPlanYearEnrollmentsEmployersRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*).
    
</dd>
</dl>

<dl>
<dd>

**benefitPlanYearId:** `String` — Unique benefit-plan-year identifier (plyr_*).
    
</dd>
</dl>

<dl>
<dd>

**electionStatus:** `Optional<ElectionStatusItem>` — Filter by election status. Repeat the parameter to match several.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `Optional<Integer>` — Items per page (default: 20, max: 100)
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number (default: 1)
    
</dd>
</dl>

<dl>
<dd>

**search:** `Optional<String>` — Case-insensitive search. Matches member name partially, and the `member_id` exactly — either your own reference id or the prefixed `grpmbr_<...>` id.
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.submitCensusSync(employerId, request) -> CensusSyncDetailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submits a census sync payload for the specified employer. The employees in the payload will be queued for processing. Returns an accepted response with the timestamp of acceptance.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().submitCensusSync(
    "empr_abc123def456",
    CensusSyncRequest
        .builder()
        .employees(
            Arrays.asList(
                CensusSyncEmployeeRequest
                    .builder()
                    .firstName("Jane")
                    .lastName("Doe")
                    .dateOfBirth("1990-05-15")
                    .email("jane.doe@acme.com")
                    .referenceId("EMP-001")
                    .phone("4155550100")
                    .address(
                        CensusSyncEmployeeAddressRequest
                            .builder()
                            .addressLine1("123 Main Street")
                            .city("San Francisco")
                            .state(State.CA)
                            .zipcode("94102")
                            .addressLine2("Apt 4B")
                            .build()
                    )
                    .startDate("2024-01-15")
                    .employeeClass(EmployeeClass.FULL_TIME)
                    .compensationType(CompensationType.SALARY)
                    .build(),
                CensusSyncEmployeeRequest
                    .builder()
                    .firstName("John")
                    .lastName("Smith")
                    .dateOfBirth("1985-11-20")
                    .email("john.smith@acme.com")
                    .phone("4155550101")
                    .startDate("2024-03-01")
                    .employeeClass(EmployeeClass.PART_TIME)
                    .compensationType(CompensationType.HOURLY)
                    .build()
            )
        )
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**employees:** `List<CensusSyncEmployeeRequest>` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.listEmployees(employerId) -> SyncPagingIterable&amp;lt;Employee&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a paginated list of employees for a specific employer. The caller must be authorized for the employer; an unknown or unauthorized employer returns 404. Results are paginated using page and limit parameters and can be narrowed with a case-insensitive `search` (first name, last name, or email) and an `employment_status` filter (active or terminated). Each employee includes payroll deductions from the most recent statement period. When a new deduction statement is generated, previous period deductions are replaced.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().listEmployees(
    "empr_abc123def456",
    ListEmployeesEmployersRequest
        .builder()
        .limit(20)
        .page(1)
        .search("jane")
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**employmentStatus:** `Optional<EmployeeStatus>` — Filter by employment status (active or terminated)
    
</dd>
</dl>

<dl>
<dd>

**limit:** `Optional<Integer>` — Items per page (default: 20, max: 100)
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number (default: 1)
    
</dd>
</dl>

<dl>
<dd>

**search:** `Optional<String>` — Case-insensitive search across employee first name, last name, and email
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.getHris(employerId) -> EmployerHrisResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the employer's HRIS connection — provider, status, last sync, and synced row count — or null when the employer has no integration. The caller must be authorized for the employer; an unknown or unauthorized employer returns 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().getHris(
    "empr_abc123def456",
    GetHrisEmployersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.listInvoices(employerId) -> EmployerInvoicesListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a cursor-paginated page of the employer's billing invoices, newest first. Pass the `next_offset` from a previous page as `offset` to fetch the next page. The caller must be authorized for the employer; an unknown or unauthorized employer returns 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().listInvoices(
    "empr_abc123def456",
    ListInvoicesEmployersRequest
        .builder()
        .limit(20)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**limit:** `Optional<Integer>` — Maximum number of invoices per page
    
</dd>
</dl>

<dl>
<dd>

**offset:** `Optional<String>` — Opaque cursor from a previous page's next_offset
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.getInvoicePdf(employerId, invoiceId) -> EmployerInvoicePdfResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the time-limited PDF download link for a single invoice belonging to the employer's billing customer. `invoice_id` is the external Chargebee id (not a prefixed UUID). The caller must be authorized for the employer; an unknown or unauthorized employer or invoice returns 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().getInvoicePdf(
    "empr_abc123def456",
    "INV-00042",
    GetInvoicePdfEmployersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**invoiceId:** `String` — External Chargebee invoice id (not a prefixed UUID).
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.getPayrollAccessSetup(employerId) -> PayrollAccessSetupStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return whether the employer has submitted payroll access setup.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().getPayrollAccessSetup(
    "empr_abc123def456",
    GetPayrollAccessSetupEmployersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.submitPayrollAccessSetup(employerId, request) -> PayrollAccessSetupStatusResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit the employer's payroll access setup answers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().submitPayrollAccessSetup(
    "empr_abc123def456",
    SubmitPayrollAccessSetupRequest
        .builder()
        .employeesInPayrollAcknowledged(true)
        .payrollDataImpactsEligibilityAcknowledged(true)
        .classificationsAccurate(true)
        .allBenefitEligibleEmployeesPresent(true)
        .isControlledGroup(true)
        .accessMethod(AccessMethod.SELF_SETUP)
        .hasAdditionalPayrollSystem(true)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>

<dl>
<dd>

**employeesInPayrollAcknowledged:** `Boolean` — Attestation that all benefit-eligible employees appear in the payroll system.
    
</dd>
</dl>

<dl>
<dd>

**payrollDataImpactsEligibilityAcknowledged:** `Boolean` — Attestation that changes to payroll data affect benefit eligibility.
    
</dd>
</dl>

<dl>
<dd>

**classificationsAccurate:** `Boolean` — Attestation that employee classifications in payroll are accurate. Set `false` to report corrections in the fields below.
    
</dd>
</dl>

<dl>
<dd>

**classificationCorrectionSource:** `Optional<ClassificationCorrectionSource>` — Where corrected classifications come from, when `classifications_accurate` is `false`.
    
</dd>
</dl>

<dl>
<dd>

**misclassifiedEmployeeNames:** `Optional<List<String>>` — Names of employees whose payroll classification needs correcting.
    
</dd>
</dl>

<dl>
<dd>

**remainingEmployeeAction:** `Optional<RemainingEmployeeAction>` — How to handle employees still missing from the payroll system.
    
</dd>
</dl>

<dl>
<dd>

**allBenefitEligibleEmployeesPresent:** `Boolean` — Attestation that every benefit-eligible employee is present in payroll.
    
</dd>
</dl>

<dl>
<dd>

**missingEmployeeResolution:** `Optional<MissingEmployeeResolution>` — How any missing employees will be added, when some are absent.
    
</dd>
</dl>

<dl>
<dd>

**isControlledGroup:** `Boolean` — Whether this employer belongs to a controlled group of related entities.
    
</dd>
</dl>

<dl>
<dd>

**samePayrollCoversOtherEins:** `Optional<Boolean>` — Whether this payroll system also covers other EINs in the controlled group.
    
</dd>
</dl>

<dl>
<dd>

**accessMethod:** `AccessMethod` 
    
</dd>
</dl>

<dl>
<dd>

**loginUrl:** `Optional<String>` — Sign-in URL for the payroll system.
    
</dd>
</dl>

<dl>
<dd>

**username:** `Optional<String>` — Username Vitable should use to access the payroll system.
    
</dd>
</dl>

<dl>
<dd>

**phone:** `Optional<String>` — Phone number used for payroll-system verification codes.
    
</dd>
</dl>

<dl>
<dd>

**password:** `Optional<String>` — Password Vitable should use to access the payroll system.
    
</dd>
</dl>

<dl>
<dd>

**integrationConfirmed:** `Optional<Boolean>` — Whether the payroll integration has been confirmed as working.
    
</dd>
</dl>

<dl>
<dd>

**hasAdditionalPayrollSystem:** `Boolean` — Whether a second payroll system is in use. When `true`, supply the `additional_*` fields below.
    
</dd>
</dl>

<dl>
<dd>

**additionalAccessMethod:** `Optional<AdditionalAccessMethod>` — How Vitable will access the second payroll system.
    
</dd>
</dl>

<dl>
<dd>

**additionalLoginUrl:** `Optional<String>` — Sign-in URL for the second payroll system.
    
</dd>
</dl>

<dl>
<dd>

**additionalUsername:** `Optional<String>` — Username Vitable should use for the second payroll system.
    
</dd>
</dl>

<dl>
<dd>

**additionalPhone:** `Optional<String>` — Phone number used for second payroll-system verification codes.
    
</dd>
</dl>

<dl>
<dd>

**additionalPassword:** `Optional<String>` — Password Vitable should use for the second payroll system.
    
</dd>
</dl>

<dl>
<dd>

**additionalIntegrationConfirmed:** `Optional<Boolean>` — Whether the second payroll integration has been confirmed as working.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.listPayrollDeductionStatements(employerId) -> SyncPagingIterable&amp;lt;PayrollDeductionStatement&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of the employer's payroll-deduction statements, newest period first, each with its period, generation date, distinct employee count, total deduction, change-file link, and deduction frequency. Statements superseded by a later correction are excluded. The caller must be authorized for the employer; an unknown or unauthorized employer returns 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().listPayrollDeductionStatements(
    "empr_abc123def456",
    ListPayrollDeductionStatementsEmployersRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**limit:** `Optional<Integer>` — Maximum number of statements per page
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number to retrieve (starts at 1)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.ensurePayrollIntegrationEmail(employerId) -> PayrollIntegrationEmailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Provision and return the employer's payroll integration email.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().ensurePayrollIntegrationEmail(
    "empr_abc123def456",
    EnsurePayrollIntegrationEmailEmployersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.updateSettings(employerId, request) -> EmployerSettingsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates configuration settings for a specific employer. The employer must belong to the authenticated organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().updateSettings(
    "empr_abc123def456",
    UpdateEmployerSettingsRequest
        .builder()
        .payFrequency(DeductionFrequency.BI_WEEKLY)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**employerId:** `String` — Unique employer identifier (empr_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>

<dl>
<dd>

**payFrequency:** `DeductionFrequency` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.employers.listHrisProviders() -> OrganizationHrisProvidersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the distinct HRIS/payroll providers across the same book `GET /v1/employers` returns, sorted for display. Use these as the values for the employers list's `hris_provider` filter — filter on `provider`, show `provider_label`. The stored providers are free text, so they cannot be enumerated in advance.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.employers().listHrisProviders(
    ListHrisProvidersEmployersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Enrollments
<details><summary><code>client.enrollments.get(enrollmentId) -> EnrollmentResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a single enrollment: the employee and employer it belongs to, the benefit product, its status, the coverage period, the employee payroll deduction and employer contribution, and the enrolled plan's Summary of Benefits and Coverage document when one is on file. An enrollment the caller cannot reach is indistinguishable from one that does not exist.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.enrollments().get(
    "enrl_AAAAAAAAAAAAAAAAAAAAAQ",
    GetEnrollmentsRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**enrollmentId:** `String` — Unique enrollment identifier (enrl_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.enrollments.reissue(enrollmentId, request) -> ReissueEnrollmentResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Closes the targeted enrollment and creates a new unanswered enrollment for the same member and plan year. VPC never requires a qualifying life event; other products require an accepted, member-owned event outside open enrollment. User-backed callers must provide a reason; it is optional for organization API-key callers. Tenant mismatches return a non-disclosing 404 before the request body is validated.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.enrollments().reissue(
    "enrl_AAAAAAAAAAAAAAAAAAAAAQ",
    ReissueEnrollmentRequest
        .builder()
        .reason("Member needs a new election after a qualifying event.")
        .ticketNumber("BPT-1234")
        .qualifyingLifeEventId("qle_AAAAAAAAAAAAAAAAAAAAAQ")
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**enrollmentId:** `String` — Unique enrollment identifier (enrl_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>

<dl>
<dd>

**reason:** `Optional<String>` — Audit reason for the reissue; required for user-backed callers and optional for long-lived organization API-key callers
    
</dd>
</dl>

<dl>
<dd>

**ticketNumber:** `Optional<String>` — Optional support or operational ticket number
    
</dd>
</dl>

<dl>
<dd>

**qualifyingLifeEventId:** `Optional<String>` — Accepted member qualifying life event identifier (qle_*)
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.enrollments.terminate(enrollmentId, request)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Terminates enrolled coverage immediately. An accepted qualifying life event owned by the enrollment member is required unless the plan is VPC or ICHRA. User-backed callers must provide a reason; it is optional for organization API-key callers. API keys may act across the caller organization's book. Tenant mismatches return the same non-disclosing 404 before the request body is validated.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.enrollments().terminate(
    "enrl_AAAAAAAAAAAAAAAAAAAAAQ",
    TerminateEnrollmentRequest
        .builder()
        .reason("Member requested coverage termination after a qualifying event.")
        .ticketNumber("BPT-1234")
        .qualifyingLifeEventId("qle_AAAAAAAAAAAAAAAAAAAAAQ")
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**enrollmentId:** `String` — Unique enrollment identifier (enrl_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>

<dl>
<dd>

**reason:** `Optional<String>` — Audit reason for the termination; required for user-backed callers and optional for long-lived organization API-key callers
    
</dd>
</dl>

<dl>
<dd>

**ticketNumber:** `Optional<String>` — Optional support or operational ticket number
    
</dd>
</dl>

<dl>
<dd>

**qualifyingLifeEventId:** `Optional<String>` — Accepted member qualifying life event identifier (qle_*)
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Groups
<details><summary><code>client.groups.list() -> SyncPagingIterable&amp;lt;Group&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of groups belonging to the authenticated organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.groups().list(
    ListGroupsRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**limit:** `Optional<Integer>` — Items per page (default: 20, max: 100)
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number (default: 1)
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.groups.create(request) -> GroupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a new group scoped to the authenticated organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.groups().create(
    CreateGroupRequest
        .builder()
        .name("Tier 1")
        .externalReferenceId("mol_seg_001")
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `String` — Display name for the group.
    
</dd>
</dl>

<dl>
<dd>

**externalReferenceId:** `String` — Your own identifier for this group. Use it to correlate the group with a record in your system; it must be unique within your organization.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.groups.get(groupId) -> GroupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a single group by its prefixed ID. Returns 404 if the group does not belong to the authenticated organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.groups().get(
    "grp_abc123def456",
    GetGroupsRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**groupId:** `String` — Unique group identifier (grp_*)
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.groups.update(groupId, request) -> GroupResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Partially updates a group's name or external reference ID. Returns 404 if the group does not belong to the authenticated organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.groups().update(
    "grp_abc123def456",
    PatchedUpdateGroupRequest
        .builder()
        .name("Tier 1 (renamed)")
        .externalReferenceId("mol_seg_001_v2")
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**groupId:** `String` — Unique group identifier (grp_*)
    
</dd>
</dl>

<dl>
<dd>

**name:** `Optional<String>` — New display name for the group. Omit to leave unchanged.
    
</dd>
</dl>

<dl>
<dd>

**externalReferenceId:** `Optional<String>` — New external reference ID for the group. Omit to leave unchanged.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Members
<details><summary><code>client.members.get(memberId) -> MemberResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a member's profile by ID — identity, demographics, address, contact details, tobacco status, and profile status. Access is scoped to the authenticated principal; a member not visible to the caller returns a 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.members().get(
    "mbr_abc123def456",
    GetMembersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**memberId:** `String` — Unique member identifier (mbr_*)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.members.listDependents(memberId) -> MemberDependentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists a member's active legal dependents — name, relationship, date of birth, age, and sex at birth. Access is scoped to the authenticated principal; a member not visible to the caller returns a 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.members().listDependents(
    "mbr_abc123def456",
    ListDependentsMembersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**memberId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.members.listEmployments(memberId) -> MemberEmploymentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists a member's employment across every employer — the same employee record shape as the employer's employees list, plus the employer name. For an organization caller the rows are scoped to companies in that organization's book; a member (self/household) or Vitable Admin sees all employments. A member not visible to the caller returns a 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.members().listEmployments(
    "mbr_abc123def456",
    ListEmploymentsMembersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**memberId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.members.listEnrollments(memberId) -> MemberEnrollmentsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists a member's benefit enrollments across every employer — benefit type and product, employer, carrier, plan, tier, employee deduction, employer contribution and total premium, the individual enrollment coverage boundary (`coverage_end`), the separate pre-effective cancellation boundary (`cancelled_date`), and the distinct benefit plan-year boundary (`plan_year_coverage_end`) used to determine whether the plan year itself has ended, the date the enrollment record was created (`issued_date`, the value Ops labels Issued on, reported for every row whatever the member answered), the window the member could answer in -- which never opens before the enrollment was issued, so a row issued mid-open-enrollment starts its window on its issue date -- whether a qualifying life event would currently be required for reissue under the product/open-enrollment rule, enrollment/open-enrollment window, and two statuses: `election_status` (what the member answered) and `policy_status` (what became of their coverage, null unless they enrolled). Every row includes a stable enrollment ID and the exact employer and benefit plan-year IDs used to fetch that row's plan-year detail. The full list is returned across all states so the client derives active plans (effective and upcoming) and the enrollment history from those per-row statuses. For an organization caller the rows are scoped to companies in that organization's book; a member (self/household) or Vitable Admin sees all enrollments. A member not visible to the caller returns a 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.members().listEnrollments(
    "mbr_abc123def456",
    ListEnrollmentsMembersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**memberId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.members.getHousehold(memberId) -> HouseholdMembersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists a member's household as a per-participant table — the account holder plus each active household member, with name, relationship, member type, date of birth, and household-admin flag. Access is scoped to the authenticated principal; a member not visible to the caller (or with no household) returns a 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.members().getHousehold(
    "mbr_abc123def456",
    GetHouseholdMembersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**memberId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.members.listIdCards(memberId) -> MemberDigitalBenefitCardsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists a member's benefit ID cards — card type (medical, dental, vision, or rx), employer, plan, provider network, claims payer, carrier contact details, and the disclaimers printed on the card. Medical, dental and vision cards come from the member's active digital benefit cards; the rx card from the member's Ventegra pharmacy benefit (omitted when the member has no free-medication coverage), which carries no plan, network, or carrier details. Access is scoped to the authenticated principal, and an organization caller sees only cards from employers in its book; a member not visible to the caller returns a 404.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.members().listIdCards(
    "mbr_abc123def456",
    ListIdCardsMembersRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**memberId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.members.listQualifyingLifeEvents(memberId) -> SyncPagingIterable&amp;lt;MemberQualifyingLifeEvent&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists a member's qualifying life events, including events already used for another enrollment. Returns all statuses by default; pass the status query param to filter to one (e.g. approved). Events are ordered newest submission first with stable paging. Custom text is present only when submitted and is otherwise null. A member not visible to the caller returns a 404. API keys and unbound access tokens have organization-wide access. Employer-bound tokens require employment at the bound employer, and employee-bound tokens require the exact employee-member relationship. Organization or scope mismatches return a 404 before pagination is validated.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.members().listQualifyingLifeEvents(
    "mbr_abc123def456",
    ListQualifyingLifeEventsMembersRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**memberId:** `String` — Unique member identifier (mbr_*)
    
</dd>
</dl>

<dl>
<dd>

**limit:** `Optional<Integer>` — Items per page (default: 20, max: 100)
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number (default: 1)
    
</dd>
</dl>

<dl>
<dd>

**status:** `Optional<Status>` — Optional. Filter to a single QLE status; omit to return all statuses.
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.members.list() -> SyncPagingIterable&amp;lt;MemberListItem&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a paginated list of the members in the authenticated organization's book — identity, contact details, and address. The book covers members reached through an employer in the organization's book as well as members of a group it owns. Supports free-text search (name, email, phone number, or exact member id).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.members().list(
    ListMembersRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**limit:** `Optional<Integer>` — Items per page (default: 20, max: 100)
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number (default: 1)
    
</dd>
</dl>

<dl>
<dd>

**search:** `Optional<String>` — Case-insensitive search across member name, email, and phone number; exact match on member id (prefixed or raw uuid)
    
</dd>
</dl>

<dl>
<dd>

**vitableOrganization:** `Optional<String>` — Organization to act as for this request (e.g. `org_SGVsbG8gV29ybGQ`). Optional when your credentials reach a single organization. Required when they reach several — omitting it then returns 400 `organization_required`. A malformed value returns 400 `invalid_organization_header`, and naming an organization you do not have access to returns 403 `organization_access_denied`.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Organizations
<details><summary><code>client.organizations.list() -> OrganizationsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Lists the organizations the authenticated caller is an active member of (paginated). Returns an empty list when the caller belongs to no organizations.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.organizations().list();
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.organizations.create(request) -> Organization</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Onboards the authenticated user's partner Organization: creates the local Organization + the creator's admin membership atomically, then mirrors it to WorkOS (creates the WorkOS org and binds the creator as admin). A user may hold several organizations and selects which one a request acts as with the `X-Vitable-Organization` header. The founder's email domain is claimed only when no other organization holds it, so a taken domain is left with its owner rather than rejected.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.organizations().create(
    CreateOrganizationRequest
        .builder()
        .name("Acme Brokerage")
        .type(CreateOrganizationRequestType.BROKERAGE)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `String` — Legal or trading name of the organization.
    
</dd>
</dl>

<dl>
<dd>

**type:** `Optional<CreateOrganizationRequestType>` — Category of organization being onboarded.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Plans
<details><summary><code>client.plans.list() -> SyncPagingIterable&amp;lt;Plan&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of benefit plans linked to the authenticated organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.plans().list(
    ListPlansRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**limit:** `Optional<Integer>` — Items per page (default: 20, max: 100)
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` — Page number (default: 1)
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhook Events
<details><summary><code>client.webhookEvents.list() -> SyncPagingIterable&amp;lt;WebhookEvent&amp;gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a paginated list of webhook events for the authenticated organization. Supports filtering by event name, resource type, resource ID, and date range.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.webhookEvents().list(
    ListWebhookEventsRequest
        .builder()
        .limit(20)
        .page(1)
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**createdAfter:** `Optional<OffsetDateTime>` 
    
</dd>
</dl>

<dl>
<dd>

**createdBefore:** `Optional<OffsetDateTime>` 
    
</dd>
</dl>

<dl>
<dd>

**eventName:** `Optional<EventName>` 

* `enrollment.accepted` - Enrollment Accepted
* `enrollment.terminated` - Enrollment Terminated
* `enrollment.termination_rescheduled` - Enrollment Termination Rescheduled
* `enrollment.elected` - Enrollment Elected
* `enrollment.granted` - Enrollment Granted
* `enrollment.waived` - Enrollment Waived
* `enrollment.started` - Enrollment Started
* `employee.eligibility_granted` - Employee Eligibility Granted
* `employee.eligibility_terminated` - Employee Eligibility Terminated
* `employee.deactivated` - Employee Deactivated
* `employee.deduction_created` - Employee Deduction Created
    
</dd>
</dl>

<dl>
<dd>

**limit:** `Optional<Integer>` 
    
</dd>
</dl>

<dl>
<dd>

**page:** `Optional<Integer>` 
    
</dd>
</dl>

<dl>
<dd>

**resourceId:** `Optional<String>` 
    
</dd>
</dl>

<dl>
<dd>

**resourceType:** `Optional<ResourceType>` 

* `enrollment` - Enrollment
* `employee` - Employee
* `employer` - Employer
* `dependent` - Dependent
* `plan_year` - Plan Year
* `payroll_deduction` - Payroll Deduction
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhookEvents.get(eventId) -> WebhookEventResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a single webhook event by its prefixed ID. Returns 404 if the event does not exist or belongs to a different organization.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.webhookEvents().get(
    "event_id",
    GetWebhookEventsRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**eventId:** `String` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhookEvents.listDeliveries(eventId) -> ListWebhookEventDeliveriesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves all delivery attempts for a webhook event. Returns up to 100 deliveries. Each delivery includes a computed status field (Pending, In Progress, Delivered, or Failed).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.webhookEvents().listDeliveries(
    "event_id",
    ListDeliveriesWebhookEventsRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**eventId:** `String` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Groups Members Sync
<details><summary><code>client.groups.members.sync.submit(groupId, request) -> GroupMemberSyncDetailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submits a member sync payload for the specified group. Members in the payload will be queued for processing asynchronously. Returns HTTP 202 with the batch ID and acceptance timestamp.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.groups().members().sync().submit(
    "grp_abc123def456",
    GroupMemberSyncRequest
        .builder()
        .members(
            Arrays.asList(
                GroupMemberSyncMemberRequest
                    .builder()
                    .referenceId("EMP-001")
                    .firstName("Jane")
                    .lastName("Doe")
                    .dateOfBirth("1990-05-15")
                    .planId("pln_abc123def456")
                    .address(
                        AddressRequest
                            .builder()
                            .addressLine1("123 Main Street")
                            .city("San Francisco")
                            .state("CA")
                            .zipcode("94102")
                            .addressLine2("Apt 4B")
                            .build()
                    )
                    .phone("4155550100")
                    .email("jane.doe@acme.com")
                    .build()
            )
        )
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**groupId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**members:** `List<GroupMemberSyncMemberRequest>` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.groups.members.sync.get(groupId, requestId) -> GroupMemberSyncRequestDetailResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieves a previously-submitted group member sync request by its `grpmsr_` ID. Returns the acceptance timestamp, completion timestamp (if processing has finished), and the per-member `results` once available. While processing is in flight, `completed_at` and `results` are `null`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```java
client.groups().members().sync().get(
    "grp_abc123def456",
    "request_id",
    GetSyncRequest
        .builder()
        .build()
);
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**groupId:** `String` 
    
</dd>
</dl>

<dl>
<dd>

**requestId:** `String` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

