Portfolio 3: Transactions and Concurrency
This portfolio shows transaction management and concurrency control in the Dove Bank Ltd database, using the accounts of James John, Ifeanyi Chime and Adejoke Samson.

COMMIT
A transaction moved ₦27,500 from James John's account to Ifeanyi Chime's account. Both balance updates and their transaction records were placed between BEGIN and COMMIT, so they were saved together as one unit. After COMMIT, James's balance was ₦285,000 and Ifeanyi's was ₦874,750, and the change stayed permanent.

ROLLBACK
A ₦60,000 withdrawal was started on Adejoke Samson's account. Inside the transaction her balance showed ₦104,300. ROLLBACK then cancelled the withdrawal, and her balance went back to ₦164,300 with no withdrawal record saved. This shows that changes can be reversed before they are committed.

Isolation
The SERIALIZABLE isolation level was used with two sessions working on Ifeanyi Chime's savings account. Session A read a balance of ₦95,800. Session B then deposited ₦12,000 and committed, but Session A still saw ₦95,800. When Session A tried to update this out-of-date value, the database stopped it with a serialization error. Session A rolled back, tried again and ended with the correct balance of ₦102,800. This stops concurrent transactions from interfering with each other and keeps the data consistent.

Concurrency Control
Two tellers tried to withdraw from James John's account at the same time, ₦15,000 and ₦8,000 from a balance of ₦285,000. Without a lock, one withdrawal was lost and the final balance was a wrong ₦277,000 (a lost update). With SELECT ... FOR UPDATE, the account record was locked, so the second teller had to wait until the first teller committed. The final balance was the correct ₦262,000, and no money was lost.
