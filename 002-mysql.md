**MySQL**
MySQL is an opensource sequel database to store data inside a structured table.

Ensure you provision a new server for MYSQL and perform the below steps in on that server and ensure you name that server as MYSQL

 Where to chose sequesl or no-sequel database depends on the type of data, application and the useCase. It's purely developer driven.
 Version of the MySQL to be installed is also an input from the developer.

**Install MySQL Server ( Version 8.0.x : As per Developer's choice )**
    # sudo dnf install mysql-server -y

**Restart Nginx Service to load the changes of the configuration.**
    # sudo systemctl enable mysqld 
    # sudo systemctl start  mysqld           
**Next, We need to change the default root password in order to start using the database service. Use password ExpenseApp@1 or any other as per your choice.**
    # sudo mysql_secure_installation --set-root-pass ExpenseApp@1

!!!! It's always recommended to configure and set up your Database before your application comes up. If not application looks for the Database and app will fail.

Once you're done, proceed with the 003-backend.md
