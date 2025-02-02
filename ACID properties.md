# ACID Properties in Database Systems

## Overview
ACID properties ensure reliable and consistent transactions in database systems. ACID stands for:

- **Atomicity**: Ensures transactions are all-or-nothing.
- **Consistency**: Guarantees database remains in a valid state.
- **Isolation**: Prevents interference between concurrent transactions.
- **Durability**: Ensures committed transactions persist permanently.

## 1. Atomicity
### Definition
A transaction is treated as a single, indivisible unit where either all operations succeed or none.

### Implementation
- Databases use transaction logs to track changes.
- If a failure occurs, the database rolls back changes.
- Savepoints allow partial rollbacks.
- SQL commands: `BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`

### Example
Transferring money between accounts: both debit and credit must succeed, or the transaction is rolled back.

### Key Point
"All or nothing."

---

## 2. Consistency
### Definition
A transaction brings the database from one valid state to another, maintaining predefined rules.

### Implementation
- Enforced through constraints (e.g., primary keys, foreign keys, unique constraints, check constraints) and triggers.
- If a transaction violates constraints, it is aborted.

### Example
An account balance cannot go below zero; a transaction violating this rule is aborted.

### Key Point
Database remains valid before and after the transaction.

---

## 3. Isolation
### Definition
Concurrent transactions do not interfere with each other, ensuring independent execution.

### Implementation
- Uses locks (row-level, table-level) or Multi-Version Concurrency Control (MVCC).
- Different isolation levels: `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE`.
- PostgreSQL command:
  ```sql
  SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
  ```

### Example
Two transactions updating the same data will not see intermediate states of each other.

### Key Point
Transactions execute independently.

---

## 4. Durability
### Definition
Once committed, a transaction's changes are permanent and survive system failures.

### Implementation
- Uses transaction logs stored in non-volatile memory.
- Write-Ahead Logging (WAL) ensures changes persist even after crashes.

### Example
After a commit, the data is saved to disk, ensuring it is not lost.

### Key Point
Committed changes are permanent.

---

## Importance of ACID Properties
- **Data Integrity**: Ensures data accuracy and consistency.
- **Reliability**: Guarantees transactions process reliably despite failures.
- **Concurrency Control**: Manages simultaneous transactions without conflicts.

### Real-World Applications
- **Banking**: Atomicity ensures complete money transfers.
- **E-commerce**: Consistency maintains correct inventory levels.

By adhering to ACID properties, databases like MySQL, PostgreSQL, and Oracle ensure robust transaction management.

