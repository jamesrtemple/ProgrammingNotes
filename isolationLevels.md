*Chaos*
The pending changes from more highly isolated transactions cannot be overwritten.

*ReadCommitted*
Volatile data cannot be read during the transaction, but can be modified.

*ReadUncommitted*
Volatile data can be read and modified during the transaction.

*RepeatableRead*
Volatile data can be read but not modified during the transaction. New data can be added during the transaction.

*Serializable*
Volatile data can be read but not modified, and no new data can be added during the transaction.

*Snapshot*
Volatile data can be read. Before a transaction modifies data, it verifies if another transaction has changed the data after it was initially read. If the data has been updated, an error is raised. This allows a transaction to get to the previously committed value of the data.
