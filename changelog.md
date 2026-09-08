## 2.1.0 - 2026-09-08
### Breaking Changes
* **`RuntimeException` thrown on serialization errors** — employer client methods (`EmployersClient`, `RawEmployersClient`, `AsyncRawEmployersClient`) now throw `RuntimeException` instead of `VitableConnectException` for serialization failures; update catch sites accordingly.
### Added
* **`vitableOrganization`** — all request types across the employers, members, and enrollments APIs now expose a `getVitableOrganization()` accessor and `vitableOrganization(String)` / `vitableOrganization(Optional<String>)` builder methods, forwarding the `X-Vitable-Organization` header to scope requests to a specific organization.
* **`ListHrisProvidersEmployersRequest`** — new request type for the HRIS/payroll providers endpoint, with optional `vitableOrganization` support for per-request organization scoping.
* **`EmployersClient.listHrisProviders(ListHrisProvidersEmployersRequest)`** — new sync and async overloads (including `RequestOptions` variants) on `EmployersClient`, `RawEmployersClient`, and `AsyncRawEmployersClient` for retrieving distinct HRIS providers.
### Changed
* **`AsyncOrganizationsClient.create()` / `AsyncRawOrganizationsClient.create()`** — Javadoc updated to reflect that a user may now hold multiple organizations and selects the active one via the `X-Vitable-Organization` header, replacing the previous single-organization restriction note.

## 2.0.0 - 2026-09-08
### Breaking Changes
* **`Operation`** has been renamed to **`GroupMemberSyncFailureOperation`**. Replace all usages of `Operation` with `GroupMemberSyncFailureOperation`, including imports, variable declarations, and references to the static constants `Operation.ADD` and `Operation.REMOVE`.
* **`GroupMemberSyncFailure.getOperation()`** now returns `GroupMemberSyncFailureOperation` instead of `Operation`. Update any code that stores or passes the return value of this method.
* **`GroupMemberSyncFailure.Builder.operation()`** now accepts `GroupMemberSyncFailureOperation` instead of `Operation`. Update builder call sites accordingly.

## 1.0.1 - 2026-09-04
* chore: remove SECURITY policy file
* Remove the SECURITY file from the repository. This file contained
* security reporting guidelines and contact information for Vitable
* Connect, but is no longer needed in the SDK.
* Key changes:
* Remove SECURITY file containing security policy and responsible disclosure guidelines
* 🌿 Generated with Fern

