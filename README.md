# Ex.No:08--Sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2 
![image](https://github.com/user-attachments/assets/7f8245e8-ad54-4ecd-9839-112d15b5ddf2)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/user-attachments/assets/dedb6bc7-af50-48c0-ac80-39192a7ced7e)
Click on the menu Login/Register and register for an account
![image](https://github.com/user-attachments/assets/666a5a40-5b3c-44d6-b8e4-1b990b8d90d6)
Click on the link “Please register here”
![image](https://github.com/user-attachments/assets/204af53f-038d-4f6c-9c36-f7dc48731c2a)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. 
Here is an outline of the page rationale:
![image](https://github.com/user-attachments/assets/52a31138-8613-48b5-87c7-f4be7288242b)
Union-based SQL injection: UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below:
![image](https://github.com/user-attachments/assets/e0cd210f-e1cb-4aa4-8906-cc891d818585)
![image](https://github.com/user-attachments/assets/2cda6cb3-e6ed-4d60-904f-f0a3854dbeef)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![image](https://github.com/user-attachments/assets/7d543502-e523-4348-a085-9e621429e16a)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.
![image](https://github.com/user-attachments/assets/c5da671f-d5df-4150-9ffd-56f1a83c5931)
The browser url of this info page need to be modified with the url as below: When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.As it is having 5 columns the query worked fine and it provides the correct resultInstead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/user-attachments/assets/c9035b53-5de8-4df8-9b52-1e4b2947128d)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database. The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table. Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
![image](https://github.com/user-attachments/assets/95e72039-2d7d-4277-901c-d1693b7fa336)













## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
