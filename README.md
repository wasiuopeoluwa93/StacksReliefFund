# Stacks Relief Fund

## Overview
This Clarity smart contract facilitates transparent and accountable donation management for beneficiaries. It enables role-based access control, donation tracking, and fund utilization approval.

## Features
- Role-based access control (Admin, Moderator, Beneficiary)
- Beneficiary registration and management
- Secure donation handling
- Utilization tracking and approval
- Transparent retrieval of donation and utilization data

## Contract Components

### Data Variables
- `contract-owner`: Stores the principal of the contract owner.
- `beneficiary-count`: Tracks the number of registered beneficiaries.
- `donation-count`: Tracks the number of donations made.
- `utilization-count`: Tracks the number of utilization entries.

### Constants
#### Error Codes
- `ERR-NOT-AUTHORIZED (u100)`: Unauthorized access.
- `ERR-ALREADY-REGISTERED (u101)`: User or entity is already registered.
- `ERR-NOT-FOUND (u102)`: Record not found.
- `ERR-INSUFFICIENT-FUNDS (u103)`: Insufficient balance for operation.
- `ERR-BENEFICIARY-NOT-FOUND (u104)`: Beneficiary does not exist.
- `ERR-UTILIZATION-NOT-FOUND (u105)`: Utilization entry not found.
- `ERR-INVALID-INPUT (u106)`: Invalid input data.

#### Role Definitions
- `ROLE-ADMIN (u1)`: Administrator with full privileges.
- `ROLE-MODERATOR (u2)`: Can manage beneficiaries.
- `ROLE-BENEFICIARY (u3)`: Can receive donations.

### Data Maps
- `roles`: Maps users to their roles.
- `beneficiaries`: Stores information on registered beneficiaries.
- `donations`: Tracks donation details.
- `utilization`: Tracks fund utilization entries.

## Functions

### Role Management
#### `set-role (user principal, new-role uint) → (ok bool | ERR-NOT-AUTHORIZED)`
Assigns a role to a user. Only the contract owner can assign roles.

#### `remove-role (user principal) → (ok bool | ERR-NOT-AUTHORIZED)`
Removes a user's role. Only the contract owner can perform this action.

### Beneficiary Management
#### `register-beneficiary (name string, description string, target-amount uint) → (ok uint | ERR-INVALID-INPUT)`
Registers a new beneficiary. Only a Moderator can register beneficiaries.

#### `get-beneficiary (id uint) → (ok {beneficiary details} | ERR-BENEFICIARY-NOT-FOUND)`
Retrieves beneficiary details by ID.

### Donation Management
#### `donate (beneficiary-id uint, amount uint) → (ok bool | ERR-INSUFFICIENT-FUNDS | ERR-INVALID-INPUT)`
Allows users to donate to a beneficiary.

#### `get-donation-by-id (donation-id uint) → (ok {donation details} | ERR-NOT-FOUND)`
Retrieves donation details by ID.

#### `get-donation-count () → (ok uint)`
Returns the total number of donations.

### Utilization Management
#### `add-utilization (beneficiary-id uint, description string, amount uint) → (ok uint | ERR-INVALID-INPUT)`
Creates a new utilization entry for a beneficiary. Only Admins can add utilization records.

#### `approve-utilization (beneficiary-id uint, milestone uint) → (ok bool | ERR-INSUFFICIENT-FUNDS | ERR-NOT-AUTHORIZED)`
Approves a utilization entry. Only Admins can approve utilization.

#### `get-utilization-by-id (utilization-id uint) → (ok {utilization details} | ERR-NOT-FOUND)`
Retrieves a utilization entry by ID.

#### `get-utilization-count () → (ok uint)`
Returns the total number of utilization entries.

### Contract Initialization
#### `initialize-contract ()`
Initializes the contract and assigns the deployer as the admin.

## Deployment & Usage
1. Deploy the contract on the Stacks blockchain.
2. The deployer is assigned the admin role automatically.
3. The admin can assign Moderator roles to manage beneficiaries.
4. Users can donate to beneficiaries via the `donate` function.
5. Admins can add and approve utilization of donated funds.

## Security Considerations
- Role-based access ensures only authorized users perform critical actions.
- Donations and utilizations are recorded transparently.
- Only Admins can approve fund utilizations to prevent misuse.

## License
This contract is open-source and can be modified to fit specific use cases.

