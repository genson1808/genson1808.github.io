# What a transaction

- A collection of queries
- One unit of work
- eg. `Account Depoiste (SELECT, UPDATE, UPDATE)`


## transaction Lifesoan
- `Transaction BEGIN` (keyword begin that indicates to the database that hey you're about to start a brand new transaction with multiple queries)
- `Transaction COMMIT` (when we are satisfied with all the queries, database actually change)
- `Transaction ROLLBACK` 
- `Transaction unexpected ending = ROLLBACK(eg. crash)`
