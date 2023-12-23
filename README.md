# DB-using-bash-script
## HOW TO RUN THE DB?
### First
##### run the following command in your bash terminal
```
sudo gedit .bashrc
```
### Second
##### in the bashrc file paste the following command 
```
export PATH=$PATH:$HOME/BashDB
```
###### note that : BashDB is a file that contains all scripts of the DB
## DB SCRIPTS DETAILS
###### The scripts are designed to run an interactive database engine in linux terminal and is built as a separate bash scripts 
###### The database is a directory in the DB directory and the tables are files that are separated by a colon : 
* ### Firstly    the user runs the database scripts that asks him to choose to apply specific operation
* #### 	Create database
this creates a new database(directory) after checking if this database exists or not
* #### 	Connect database
  this shows the user the names of the existing database and  connects him/her to an existing database after checking its existence
* ####  List database
  lists the tables(files) that are in the database
* ####  Remove database
  removes the database after prompting the user to enter y
* #### 	Exit
  exit the code
* #### When creating a database we need to check whether the name of the new database comes with the naming conventions of the database (eg. Doesn’t start with a number,doesn’t contain spaces) using a new defined function **“validate_name”**
* #### This menu is handled via  “select” command in bash with the aid of “case” we use “while true” loop to ensure that the menu appears until the user exit or go to the connect database menu
* ### Secondly, after the user connects to a specific database he/she is redirected to a new menu that has some table options
* #### Create table
  when creating a table the user is asked about table name that is validated using **“validate_name”**  and then the user is asked about the number of columns and each column name and type(either string or integer) this info is saved in a file called meta_data and handled via a **“for”** loop, The names of the tables created are saved in a file called “tables_name” which will be used later to display tables , the first table is assumed to be the primary key by default 
* #### List table
  this lists all tables in the database using **“cat”** command on the “tables_name” file
* #### Drop table
  displays the tables and allows the user to drop the whole table via removing the “data” and “meta_data” files and deleting the the table name from the **“tables_name”** file via **“awk”** and **“sed”** utility with the aid of “if” condition to assure that user entered a a valid option 
* #### Insert to table
  displays the tables to choose from and then display each column to insert into with a check to make sure if the column is the first one (PK) or not
   * if it’s the PK then we need to assure that it’s unique,not null and integer and these conditions are handled via **“if”** conditions and **“while true”** to keep asking the user for the new value until the user enters a valid value.
   * if it is not PK then we need to check whether it’s an integer of string 
   * in case of integer , we need to check if the new value is intger or not and if it’s not , we keep asking the user until entering a valid new value
   * string column are allowed to be string or integer
   * The new inserted row is appended to the data file using **“tee”** 

* #### Select table
after displaying the tables and choosing one table the user is asked to choose either to “select all” “select a column” “select row by a column” “back” to go back to the previous menu, selecting all row is just a **“cat”** on the data file while selecting a row or a column is handled via **“awk”** utility 
* #### Delete from table
Delete from table: it deletes from the table based on the option the user will choose from the provided menu (Delete all rows, Delete one row based on column or Exit the whole menu and return to the main page) deleting all rows is just a redirection of the header row to temporary file and then to the data file using **“cp”** and **“awk”** commands while deleting one row based on column uses **“awk”** utility besides an **“if”** condition to print only lines that don’t match a specific value and exclude the line to be deleted then redirect the output to a temporary file and then to the data file
* #### Update table
updates the content of the table starting from displaying all the tables available in  the DB and let the user choose the desired one and check if the number of the table inserted by the user exists or not  and then display a menu to choose (Replace All, Replace based on one column ,Back to previous menu). If the user chooses Replace All it will make sure that the PK is not replaced and keeps it away in another file, if the user chooses Replace based on one column and he/she wants to replace on PK it will make sure that the new_value will be unique and integer and not null , if the updated column is of type integer , we will check first that the new value is integer , if not , we will keep asking the user until entering a valid value
* #### Drop column
it displays all the tables available in the DB to the user first and then ask for the number of the table desired after that it displays all the columns available in this table and the user chooses the number he/she want to drop this column from the data and metadata files , dropping the column is done via a new defined function **“drop_column”** that takes two argument the line and the field number and combine **“split”**,**”awk”**,**”for”** loop to split the line into fields based on the delimiter :  and check if the field isn’t the last one and then the next fields isn’t empty and then adds a colon after the field value then substitute each double colons  :: by a colon  : . the user is asked whether he/she wants to go the tables menu or the database menu
* #### Back to previous menu
it redirects the user back to the main page    

DON'T HESITATE TO CONTACT US IF YOU FACE ANY PROBLEM WHILE RUNNING THE SCRIPTS :) :) :)



