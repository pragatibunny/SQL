# SQL Assignment

    
1.Write a query to display account number, customer’s number, customer’s firstname,lastname,account opening date.
Display the records sorted in ascending order based on account number.

SELECT account_number,am.customer_number,firstname,lastname,account_opening_date
FROM customer_master cm INNER JOIN account_master am
ON cm.customer_number=am.customer_number
ORDER BY account_number

2.Write a query to display the number of customer’s from Chennai. Give the count an alias name of Cust_Count.
SELECT count(customer_number) Cust_Count
FROM customer_master
WHERE customer_city='Chennai'

3.Write a query to display the customer number, customer firstname,account number for the customer’s whose accounts were created after 15th of any month.
Display the records sorted in ascending order based on customer number and then by account number.
SELECT am.customer_number, firstname, account_number
FROM customer_master cm INNER JOIN account_master am
ON cm.customer_number=am.customer_number
WHERE extract(day from account_opening_date)>15
ORDER BY am.customer_number, account_number

4.Write a query to display the number of customers who have registration but no account in the bank.
Give the alias name as Count_Customer for number of customers.
SELECT count(customer_number) Count_Customer
FROM customer_master
WHERE customer_number NOT IN (SELECT customer_number FROM account_master)

5.Write a query to display the firstname of the customers who have more than 1 account. Display the records in sorted order based on firstname.
select firstname
FROM customer_master cm INNER JOIN account_master am ON cm.customer_number=am.customer_number group by firstname having count(account_number)>1 order by firstname;
    
6.Write a query to display the number of clients who have asked for loans but they don’t have any account in the bank though they are registered customers. Give the count an alias name of Count.
SELECT count(ld.customer_number) Count
FROM customer_master cm INNER JOIN loan_detailsld
ON cm.customer_number=ld.customer_number
WHERE cm.customer_number NOT IN ( SELECTcustomer_number FROM account_master)

7.Write a query to display the customer’s firstname who have multiple accounts (atleast 2 accounts). Display the records sorted in ascending order based on customer's firstname.
SELECT firstname
FROM customer_master INNER JOIN account_master
ON customer_master.customer_number=account_master.customer_number GROUP BY firstname
having count(firstname)>=2 order by firstname;
