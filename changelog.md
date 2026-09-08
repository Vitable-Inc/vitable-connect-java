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

