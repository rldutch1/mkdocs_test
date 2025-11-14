#<h1>Terminology:</h1>
###### Data Definition Language (DDL):
- DDL statements are used to define the database structure or schema. DDL (Data Definition Language) refers to the **CREATE, ALTER and DROP** statements
- DDL allows to add / modify / delete the logical structures which contain the data or which allow users to access / maintain the data (databases, tables, keys, views...). DDL is about "metadata".
- Some examples:
	- CREATE - to create objects in the database
	- ALTER - alters the structure of the database
	- DROP - delete objects from the database
	- TRUNCATE - remove all records from a table, including all spaces allocated for the records are removed. The operation cannot be rolled back.
	- COMMENT - add comments to the data dictionary
	- RENAME - rename an object

###### Data Manipulation Language (DML):
- DML (Data Manipulation Language) refers to the **INSERT, UPDATE and DELETE** statements.
- DML statements are used for managing data within schema objects.
- DML allows to add / modify / delete data itself.

- Some examples:
	- INSERT - insert data into a table
	- UPDATE - updates existing data within a table
	- DELETE - deletes all records from a table, the space for the records remain. Can be rolled back. Must me committed to make changes permanent.
	- MERGE - UPSERT operation (insert or update)
	- CALL - call a PL/SQL or Java subprogram
	- EXPLAIN PLAN - explain access path to data
	- LOCK TABLE - control concurrency

###### DQL (Data Query Language):
- DQL refers to the **SELECT, SHOW and HELP** statements (queries)
- **SELECT** is the main DQL instruction. It retrieves data you need. SHOW retrieves information about the metadata. **HELP**... is for people who need help.

- Some examples:
	- SELECT - retrieve data from the a database

###### Data Control Language (DCL):
- DCL (Data Control Language) refers to the **GRANT and REVOKE** statements
- DCL is used to grant / revoke permissions on databases and their contents. DCL is simple, but MySQL's permissions are rather complex. DCL is about security.

- Some examples:
	- GRANT - gives user's access privileges to database
	- REVOKE - withdraw access privileges given with the GRANT command

###### Transaction Control (TCL):
- TCL statements are used to manage the changes made by DML statements. It allows statements to be grouped together into logical transactions.
	- COMMIT - save work done
	- SAVEPOINT - identify a point in a transaction to which you can later roll back
	- ROLLBACK - restore database to original since the last COMMIT
	- SET TRANSACTION - Change transaction options like isolation level and what rollback segment to use

###### DTL (Data Transaction Language):
- DTL refers to the **START TRANSACTION, SAVEPOINT, COMMIT and ROLLBACK [TO SAVEPOINT]** statements.
- DTL is used to manage transactions (operations which include more instructions none of which can be executed if one of them fails).


###### Note about DROP, TRUNCATE, and DELETE:
**DROP and TRUNCATE** are DDL commands, whereas **DELETE* is a DML command. Therefore **DELETE** operations can be rolled back (undone), while **DROP** and TRUNCATE operations cannot be rolled back.

#### MySQL Data Types:

    Properly defining the fields in a table is important to the overall optimization of your database. You should use only the type and size of field you really need to use; don't define a field as 10 characters wide if you know you're only going to use 2 characters. These types of fields (or columns) are also referred to as data types, after the type of data you will be storing in those fields.

    MySQL uses many different data types broken into three categories: numeric, date and time, and string types.

    - Numeric Data Types: MySQL uses all the standard ANSI SQL numeric data types, so if you're coming to MySQL from a different database system, these definitions will look familiar to you. The following list shows the common numeric data types and their descriptions:
    	- INT - A normal-sized integer that can be signed or unsigned. If signed, the allowable range is from -2147483648 to 2147483647. If unsigned, the allowable range is from 0 to 4294967295. You can specify a width of up to 11 digits.
    	- TINYINT - A very small integer that can be signed or unsigned. If signed, the allowable range is from -128 to 127. If unsigned, the allowable range is from 0 to 255. You can specify a width of up to 4 digits.
    	- SMALLINT - A small integer that can be signed or unsigned. If signed, the allowable range is from -32768 to 32767. If unsigned, the allowable range is from 0 to 65535. You can specify a width of up to 5 digits.
    	- MEDIUMINT - A medium-sized integer that can be signed or unsigned. If signed, the allowable range is from -8388608 to 8388607. If unsigned, the allowable range is from 0 to 16777215. You can specify a width of up to 9 digits.
    	- BIGINT - A large integer that can be signed or unsigned. If signed, the allowable range is from -9223372036854775808 to 9223372036854775807. If unsigned, the allowable range is from 0 to 18446744073709551615. You can specify a width of up to 20 digits.
    	- FLOAT(M,D) - A floating-point number that cannot be unsigned. You can define the display length (M) and the number of decimals (D). This is not required and will default to 10,2, where 2 is the number of decimals and 10 is the total number of digits (including decimals). Decimal precision can go to 24 places for a FLOAT.
    	- DOUBLE(M,D) - A double precision floating-point number that cannot be unsigned. You can define the display length (M) and the number of decimals (D). This is not required and will default to 16,4, where 4 is the number of decimals. Decimal precision can go to 53 places for a DOUBLE. REAL is a synonym for DOUBLE.
    	- DECIMAL(M,D) - An unpacked floating-point number that cannot be unsigned. In unpacked decimals, each decimal corresponds to one byte. Defining the display length (M) and the number of decimals (D) is required. NUMERIC is a synonym for DECIMAL.
    	- Date and Time Types: The MySQL date and time datatypes are:
    	- DATE - A date in YYYY-MM-DD format, between 1000-01-01 and 9999-12-31. For example, December 30th, 1973 would be stored as 1973-12-30.
    	- DATETIME - A date and time combination in YYYY-MM-DD HH:MM:SS format, between 1000-01-01 00:00:00 and 9999-12-31 23:59:59. For example, 3:30 in the afternoon on December 30th, 1973 would be stored as 1973-12-30 15:30:00.
    	- TIMESTAMP - A timestamp between midnight, January 1, 1970 and sometime in 2037. This looks like the previous DATETIME format, only without the hyphens between numbers; 3:30 in the afternoon on December 30th, 1973 would be stored as 19731230153000 ( YYYYMMDDHHMMSS ).
    	- TIME - Stores the time in HH:MM:SS format.
    	- YEAR(M) - Stores a year in 2-digit or 4-digit format. If the length is specified as 2 (for example YEAR(2)), YEAR can be 1970 to 2069 (70 to 69). If the length is specified as 4, YEAR can be 1901 to 2155. The default length is 4.

    - String Types: Although numeric and date types are fun, most data you'll store will be in string format. This list describes the common string datatypes in MySQL.
    	- CHAR(M) - A fixed-length string between 1 and 255 characters in length (for example CHAR(5)), right-padded with spaces to the specified length when stored. Defining a length is not required, but the default is 1.
    	- VARCHAR(M) - A variable-length string between 1 and 255 characters in length; for example VARCHAR(25). You must define a length when creating a VARCHAR field.
    	- BLOB or TEXT - A field with a maximum length of 65535 characters. BLOBs are "Binary Large Objects" and are used to store large amounts of binary data, such as images or other types of files. Fields defined as TEXT also hold large amounts of data; the difference between the two is that sorts and comparisons on stored data are case sensitive on BLOBs and are not case sensitive in TEXT fields. You do not specify a length with BLOB or TEXT.
    	- TINYBLOB or TINYTEXT - A BLOB or TEXT column with a maximum length of 255 characters. You do not specify a length with TINYBLOB or TINYTEXT.
    	- MEDIUMBLOB or MEDIUMTEXT - A BLOB or TEXT column with a maximum length of 16777215 characters. You do not specify a length with MEDIUMBLOB or MEDIUMTEXT.
     	- LONGBLOB or LONGTEXT - A BLOB or TEXT column with a maximum length of 4294967295 characters. You do not specify a length with LONGBLOB or LONGTEXT.
    	- ENUM - An enumeration, which is a fancy term for list. When defining an ENUM, you are creating a list of items from which the value must be selected (or it can be NULL). For example, if you wanted your field to contain "A" or "B" or "C", you would define your ENUM as ENUM ('A', 'B', 'C') and only those values (or NULL) could ever populate that field.
    Source: http://www.tutorialspoint.com/mysql/mysql-data-types.htm

#### Alter Table:
###### Alter Table Column (CHANGE and MODIFY):
- CHANGE allows you to rename a column and change the definition.
- MODIFY allows you to change the definition (cannot rename).

	- Rename a table column named tasklist to entry:

	``` ALTER TABLE tablename CHANGE tasklist entry MEDIUMTEXT NOT NULL; ```

	- Alter the column definition:

	```	alter table tablename modify column1 timestamp not null default current_timestamp on update current_timestamp; ```

	- Alter the table field type and comment:

	```	ALTER TABLE  `weapons` CHANGE  `active_ind`  `active_ind` TINYINT( 1 ) UNSIGNED NOT NULL DEFAULT  '0' COMMENT  '1 Disposed, 0 Not Disposed'; ```

###### Alter Table (Add):
- Adding columns to a table.
	- Adding a single colum to a table:

	``` ALTER TABLE tablename add column columnname varchar(100) not null after id; ```

	- Making a column unique:

	```ALTER TABLE tablename add unique (column1); ```

	- Giving the unique index a name:

	``` ALTER TABLE tablename add unique idx_uniquename (column1); ```

	- Multi-column unique index with a name:
	Source: https://stackoverflow.com/questions/635937/how-do-i-specify-unique-constraint-for-multiple-columns-in-mysql

	``` ALTER TABLE `tablename` add unique `idx_unique_index_name`(`column1`, `column2`, `column3`); ```

###### Alter Table (Move a column):

	``` ALTER TABLE `tablename` CHANGE `columnname` `columname` INT(11) NOT NULL AFTER `someothercolumnname`; ```

	- Example: Move the lastname column after the firstname column in the customers table.

	``` ALTER TABLE `customers` CHANGE `lastname` `lastname` INT(11) NOT NULL AFTER `firstname`; ```

###### Create a unique index with a name and a comment (MySQL v8):
- Try to use idx for beginning of index name.
	- Syntax: Create unique index:

	 ``` CREATE UNIQUE INDEX `idx_videos_videoname`  ON `videos`.`videos` (videoname) COMMENT 'Unique videoname' ALGORITHM DEFAULT LOCK DEFAULT ```

** You might get ERROR 1062 Duplicate entry '' for key ??? if
the column you are trying to make unique, already has duplicate data. This includes
NULL and spaces. **

- Removing the unique index.
	- Syntax: Notice the missing parenthesis:

	```ALTER TABLE tablename drop index column1; ```

###### Remove the primary key:
- Without an index, maintaining an autoincrement column becomes too expensive, that's why MySQL requires an autoincrement column to be a leftmost part of an index.
	- Syntax: You should remove the autoincrement property before dropping the key:

	```ALTER TABLE tablename MODIFY id INT NOT NULL; -- Removing autoincrement.```

	```ALTER TABLE tablename DROP PRIMARY KEY;```

###### Set field value to default to nothing instead of NULL:

	alter table customers modify address2 varchar(100) null default "";


###### Rename a MySQL table:
- The "to" keyword is part of the command.
	- Syntax:

	```rename table oldtable to newtable; ```

###### Rename a Database:
- For InnoDB, the following seems to work: create the new empty database, then rename each table and turn into the new database:
	- Syntax:

	```RENAME TABLE old_db.table TO new_db.table; ```

- You will need to adjust the permissions after that.

For scripting in a shell, you can use either of the following:

- This:

	```mysql -u username -ppassword old_db -sNe 'show tables' | while read table; \
    do mysql -u username -ppassword -sNe "rename table old_db.$table to new_db.$table"; done ```

- Or:

	```for table in `mysql -u root -s -N -e "show tables from old_db"\`; do mysql -u root -s -N -e "rename table old_db.$table to new_db.$table"; done;` ```

- **Note:** there is no space between the option -p and the password. If your database user has no password, remove the -u username -ppassword part.

- If you have stored procedures, you can copy them afterward:

#### Alter User:

###### Change Password / Lock and Unlock Accounts:

    use mysql;
    -- Method 1 (Deprecated):
    update mysql.user set password("thepassword123") where user = 'hillc';
    FLUSH PRIVILEGES;

    -- Method 2 (MySQL 5.7+):
    update mysql.user set authentication_string=PASSWORD("thepassword123") where user='hillc';
    FLUSH PRIVILEGES;

    -- Method 3 (Preferred method for current user.):
    alter user set password = "thepassword123";
    FLUSH PRIVILEGES;

    -- MySQL 5.7:
    alter user 'hillc'@'localhost' identified by "thepassword123";
    alter user 'hillc'@'%' identified by "thepassword123";

    -- Method 4 (Preferred method for another user.):
    alter user set password for 'hillc'@'localhost' = "thepassword123";
    FLUSH PRIVILEGES;

    -- Remote user password change:
    alter user set password for 'hillc'@'%' = "thepassword123";
    FLUSH PRIVILEGES;


    -- ALTER USER ==
    ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.

    --If you started MySQL using "mysql -u root -p" use this method to reset your password:
    	ALTER USER 'root'@'localhost' IDENTIFIED BY 'Your New Password';

    -- This worked for me from the MySQL DB prompt:
    	SET PASSWORD = PASSWORD("your_new_password");

    -- Source: http://stackoverflow.com/questions/33467337/reset-mysql-root-password-using-alter-user-statement-after-install-on-mac

    -- This syntax enables changing your own password without naming your account literally.
    	ALTER USER USER() IDENTIFIED BY "auth_string";

    -- This statement changes the password for jeffrey but leaves that for jeanne unchanged. For both accounts, connections are required to use SSL and -- each account can be used for a maximum of two simultaneous connections:
    	ALTER USER
      	'jeffrey'@'localhost' IDENTIFIED BY "new_password",
      	'jeanne'@'localhost'
      	REQUIRE SSL WITH MAX_USER_CONNECTIONS 2;

    -- Example 1: Change an account's password and expire it. As a result, the user must connect with the named password and choose a new one at the next connection:
    	ALTER USER 'jeffrey'@'localhost'
      	IDENTIFIED BY "new_password" PASSWORD EXPIRE;

    -- Example 2: Modify an account to use the sha256_password authentication plugin and the given password. Require that a new password be chosen every 180 days:
    	ALTER USER 'jeffrey'@'localhost'
      	IDENTIFIED WITH sha256_password BY "new_password"  (SHA256 may require an SSL connection on some systems)
      	PASSWORD EXPIRE INTERVAL 180 DAY;

    -- Example 3: Lock or unlock an account:
    	ALTER USER 'jeffrey'@'localhost' ACCOUNT LOCK;
    		ALTER USER 'jeffrey'@'localhost' ACCOUNT UNLOCK;

    -- Example 4: Require an account to connect using SSL and establish a limit of 20 connections per hour:
    	ALTER USER 'jeffrey'@'localhost'
      	REQUIRE SSL WITH MAX_CONNECTIONS_PER_HOUR 20;

    -- http://dev.mysql.com/doc/refman/5.7/en/alter-user.html

    -- Lock User Account on MySQL 8.0.x.x.:
    UPDATE `user` SET `account_locked` = 'Y' WHERE `user`.`Host` = 'localhost' AND `user`.`User` = 'robdba5';

    -- Solution for - Connect Error: SQLSTATE[HY000] [2054] The server requested authentication method unknown to the client.
    -- Change the authentication method from auth_socket to mysql_native_password:
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY "password";

    --  Switch to caching_sha2_password authentication for MySQL 8 upgrades:
      ALTER USER 'umptyfratz'@'%'
        IDENTIFIED WITH caching_sha2_password
        BY "password";

      ALTER USER 'root'@'localhost'
        IDENTIFIED WITH mysql_native_password
        BY "password";

###### Show create user:
```
	show create user billybob@localhost;
```

#### Blob (text) data display using convert(FIELD using utf8mb4):
```
	-- I used this in my bacula database to find jobs that contained the file groupmems.
		SELECT DISTINCT Job.JobId as JobId, convert(Client.Name using utf8mb4) as Client,
		  convert(Path.Path using utf8mb4),convert(File.FileName using utf8mb4),StartTime,Level,JobFiles,JobBytes
		 FROM Client,Job,File,Path
		 WHERE Client.ClientId=Job.ClientId
		 AND JobStatus IN ('T','W')
		 AND Job.JobId=File.JobId
		 AND Path.PathId=File.PathId
		 AND convert(File.FileName using utf8mb4) = 'groupmems'
		 AND File.FileIndex > 0
		 -- AND Job.JobId = 16
		 ORDER BY Job.StartTime;
```

#### CHAR_LENGTH:
###### Needed to find out the maximum length of each column so that I could dynamically adjust the column width in PDF output. This shows the maximum length of the manufacturer_importer column.
				select inventory_number, manufacturer_importer, max(char_length(`manufacturer_importer`)) Number_of_Characters from vw_ffl_book2 group by manufacturer_importer, inventory_number order by Number_of_Characters desc;

###### This shows me the maximum length of the model column from highest to lowest.
				select model, max(char_length(`model`)) Number_of_Characters from vw_ffl_book2 group by model order by Number_of_Characters desc;


#### Concatinate:

    This is a query that I used to sequentially rename some video files so they would be in the
    correct order. I accidentally numbered them 1 to 32 and they were in alphabetical order instead
    of chronological order. I had to renumber them so they would be in chronolocial order:

    I used the concat and substring_index functions:

    	select concat('mv ',oldname,' ',newnum,'.',substring_index(oldname,'.',-2)) as Rename_Script from v_rename;


    Concatenate multiple MySQL rows into one field?
    You can use GROUP_CONCAT:

    SELECT person_id, GROUP_CONCAT(hobbies SEPARATOR ', ')
    FROM peoples_hobbies
    GROUP BY person_id;
    As Ludwig stated in his comment, you can add the DISTINCT operator to avoid duplicates:

    SELECT person_id, GROUP_CONCAT(DISTINCT hobbies SEPARATOR ', ')
    FROM peoples_hobbies
    GROUP BY person_id;
    As Jan stated in their comment, you can also sort the values before imploding it using ORDER BY:

    SELECT person_id, GROUP_CONCAT(hobbies ORDER BY hobbies ASC SEPARATOR ', ')
    FROM peoples_hobbies
    GROUP BY person_id;
    As Dag stated in his comment, there is a 1024 byte limit on the result. To solve this, run this query before your query:

    SET group_concat_max_len = 2048;
    Of course, you can change 2048 according to your needs. To calculate and assign the value:

    SET group_concat_max_len = CAST(
        (SELECT SUM(LENGTH(hobbies)) + COUNT(*) * LENGTH(', ')
        FROM peoples_hobbies
        GROUP BY person_id)
        AS UNSIGNED
    );

    Source: https://stackoverflow.com/questions/276927/can-i-concatenate-multiple-mysql-rows-into-one-field?rq=1

#### Conditional Update:

    create table test (
    id int not null auto_increment primary key,
    name varchar(50),
    age tinyint
    ) engine = myisam;

    insert into test (name) values ("jim"),("john"),("paul"),("mike");

    - The age field is now NULL.
    select * from test;

    update test
    set age =
    case
    when name = "jim" then 10
    when name = "paul" then 20
    else 30
    end;

    - The age field now has data.
    select * from test;

#### Create a Stored Procedure:

###### Create a stored procedure that inserts 10 rows

    DELIMITER $$

    DROP PROCEDURE IF EXISTS insert_ten_rows $$

    CREATE PROCEDURE insert_ten_rows ()
    BEGIN
    DECLARE crs INT DEFAULT 0;

    WHILE crs < 10 DO
    INSERT INTO `continent`(`name`) VALUES ('count_'+crs);
    SET crs = crs + 1;
    END WHILE;
    END $$

    DELIMITER ;Invoke the procedure:

    CALL insert_ten_rows();

#### Create Users:
###### Syntax definitions:
        % = remote user
        localhost = local user on server/computer


###### This is my MySQL Create User Statement:
    CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
		-- ALTER USER 'theusername'@'localhost' IDENTIFIED BY 'some_pass';
    GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost'
    WITH GRANT OPTION;

    CREATE USER 'monty'@'%' IDENTIFIED BY 'some_pass';
    GRANT ALL PRIVILEGES ON *.* TO 'monty'@'%'
    WITH GRANT OPTION;

###### This is my MariaDB Create User and MySQL Create User Statement.
    CREATE USER 'SomeUser'@'%';
    CREATE USER 'SomeUser'@'localhost';
    SET PASSWORD FOR 'SomeUser'@'%' = PASSWORD('SomePassword!');
    SET PASSWORD FOR 'SomeUser'@'localhost' = PASSWORD('SomePassword!');
    GRANT USAGE ON SomeDatabase.* TO 'SomeUser'@'localhost'
    GRANT USAGE ON SomeDatabase.* TO 'SomeUser'@'%'
    REQUIRE NONE
    WITH MAX_QUERIES_PER_HOUR 0
    MAX_CONNECTIONS_PER_HOUR 0
    MAX_UPDATES_PER_HOUR 0
    MAX_USER_CONNECTIONS 0;
    GRANT ALL PRIVILEGES ON `SomeDatabase`.* TO 'SomeUser'@'localhost';
    GRANT ALL PRIVILEGES ON `SomeDatabase\_%`.* TO 'SomeUser'@'%';
    FLUSH PRIVILEGES;

    On MariaDB: I got an access denied error when I tried to run the following statement as root.
        UPDATE mysql.user SET Grant_priv='Y', Super_priv='Y' WHERE User='rob';
        FLUSH PRIVILEGES;

    I had to run the following as root to give myself the "GRANT" privilege. (https://stackoverflow.com/questions/8484722/access-denied-for-user-rootlocalhost-while-attempting-to-grant-privileges)
    Note that we use `%`.* instead of *.* <-- The backticks are needed.
    Website example: GRANT ALL PRIVILEGES ON `%`.* TO '[user]'@'[hostname]' IDENTIFIED BY '[password]' WITH GRANT OPTION;
    I ran it without the password section because I already have an established password:
      GRANT ALL PRIVILEGES ON `%`.* TO 'rob'@'localhost' WITH GRANT OPTION;
      GRANT ALL PRIVILEGES ON *.* TO 'rob'@'%' WITH GRANT OPTION;

    MySQL 8.0.X.X. Create user with mysql_native_password authentication;
    CREATE USER username@localhost identified with mysql_native_password by 'password';

###### VPS on Godaddy;
		CREATE USER 'theusername'@'localhost';
		ALTER USER 'theusername'@'localhost' IDENTIFIED BY 'thePa55word!' -- MySQL
		GRANT USAGE ON thedatabase.* TO 'theusername'@'localhost';
		GRANT ALL PRIVILEGES ON `thedatabase`.* TO 'theusername'@'localhost';
		GRANT ALL PRIVILEGES ON `thedatabase\_%`.* TO 'theusername'@'localhost';

#### Datatypes Example:
    --Create a table with all of the MySQL datatypes.
    CREATE TABLE`all_data_types` (
        `bigint` BIGINT,
        `binary` BINARY( 20 ),
        `blob` BLOB,
        `bool` BOOL,
        `char` CHAR( 10 ),
        `date` DATE,
        `datetime` DATETIME,
        `decimal` DECIMAL( 10, 2 ),
        `double` DOUBLE,
        `enum` ENUM( '1', '2', '3' ),
        `float` FLOAT( 10, 2 ),
        `int` INT,
        `longblob` LONGBLOB,
        `longtext` LONGTEXT,
        `mediumblob` MEDIUMBLOB,
        `mediumint` MEDIUMINT,
        `mediumtext` MEDIUMTEXT,
        `set` SET( '1', '2', '3' ),
        `smallint` SMALLINT,
        `text` TEXT,
        `timestamp` TIMESTAMP,
        `time` TIME,
        `tinyblob` TINYBLOB,
        `tinyint` TINYINT,
        `tinytext` TINYTEXT,
        `varbinary` VARBINARY( 20 ),
        `varchar` VARCHAR( 20 ),
        `year` YEAR
    ) ENGINE= innodb ;


###### Date fields:
    MySQL Reference Manual - Date Time Functions
    Date Add:
    mysql> SELECT DATE_ADD('2018-05-01',INTERVAL 1 DAY);
            -> '2018-05-02'
    mysql> SELECT DATE_SUB('2018-05-01',INTERVAL 1 YEAR);
            -> '2017-05-01'
    mysql> SELECT DATE_ADD('2020-12-31 23:59:59',
        ->                 INTERVAL 1 SECOND);
            -> '2021-01-01 00:00:00'
    mysql> SELECT DATE_ADD('2018-12-31 23:59:59',
        ->                 INTERVAL 1 DAY);
            -> '2019-01-01 23:59:59'
    mysql> SELECT DATE_ADD('2100-12-31 23:59:59',
        ->                 INTERVAL '1:1' MINUTE_SECOND);
            -> '2101-01-01 00:01:00'
    mysql> SELECT DATE_SUB('2025-01-01 00:00:00',
        ->                 INTERVAL '1 1:1:1' DAY_SECOND);
            -> '2024-12-30 22:58:59'
    mysql> SELECT DATE_ADD('1900-01-01 00:00:00',
        ->                 INTERVAL '-1 10' DAY_HOUR);
            -> '1899-12-30 14:00:00'
    mysql> SELECT DATE_SUB('1998-01-02', INTERVAL 31 DAY);
            -> '1997-12-02'
    mysql> SELECT DATE_ADD('1992-12-31 23:59:59.000002',
        ->            INTERVAL '1.999999' SECOND_MICROSECOND);
            -> '1993-01-01 00:00:01.000001'

    Date Difference:
    mysql> SELECT DATEDIFF('2007-12-31 23:59:59','2007-12-30');
            -> 1
    mysql> SELECT DATEDIFF('2010-11-30 23:59:59','2010-12-31');
            -> -31

    select year(date_field) as year from table;

###### Difference between DATETIME and TIMESTAMP:

    --The timestamp data type has a limitation between the years 1970 and 2038.
    --Use datetime instead. If you need a timestamp you can set the default to current_timestamp.
    --See the updt_dt_tm and cr_date fields in the table below.

    CREATE TABLE `test1` (
      `id` int(11) NOT NULL AUTO_INCREMENT,
      `firstname` varchar(100) NOT NULL,
      `lastname` varchar(100) NOT NULL,
      `updt_dt_tm` datetime DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
      `cr_date` datetime DEFAULT CURRENT_TIMESTAMP,
      PRIMARY KEY (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=latin1;

    --Date Format:
    	http://www.mysqltutorial.org/mysql-date/

    -- Alter table and add a datetime column that defaults to the current timestamp.
    alter table code_value add column updt_dt_tm datetime not null default current_timestamp on update current_timestamp;

#### DEFINER Change:
##### Change/Update DEFINER:
    1. Change the DEFINER

    This is possibly easiest to do when initially importing your database objects, by removing any DEFINER statements from the dump.

    Changing the definer later is a little more tricky:

    How to change the definer for views

    Run this SQL to generate the necessary ALTER statements
    SELECT CONCAT("ALTER DEFINER=`youruser`@`host` VIEW ",
    table_name, " AS ", view_definition, ";")
    FROM information_schema.views
    WHERE table_schema='your-database-name';
    Copy and run the ALTER statements


    How to change the definer for stored procedures

    Example:

    UPDATE `mysql`.`proc` p SET definer = 'user@%' WHERE definer='root@%'
    Be careful, because this will change all the definers for all databases.

    2. Create the missing user

    If you've found following error while using MySQL database:

    The user specified as a definer ('someuser'@'%') does not exist`
    Then you can solve it by using following :

    GRANT ALL ON *.* TO 'someuser'@'%' IDENTIFIED BY 'complex-password';
    FLUSH PRIVILEGES;
    From http://www.lynnnayko.com/2010/07/mysql-user-specified-as-definer-root.html

    This worked like a charm - you only have to change someuser to the name of the missing user. On a local dev server, you might typically just use root.

    Also consider whether you actually need to grant the user ALL permissions or whether they could do with less.

    ********************
    select concat("ALTER DEFINER=`rlholland1`@`localhost` VIEW ", weapons, " AS " , view_definition, ";") FROM information_schema.views where table_schema="hillc1";

#### DROP
###### Drop a database:

				drop database `TheDataBaseName`;

###### Drop a table;

				drop table `TheTablename`;

###### Drop an index:

				alter TheTableName drop `TheIndexName`;

######** In MySQL, theres no DROP CONSTRAINT, you have to use DROP FOREIGN KEY instead:

		ALTER TABLE `table_name`
		DROP FOREIGN KEY `id_name_fk`;
		You might have to drop the index too because simply removing the foreign key does not remove the index.

		ALTER TABLE `table_name`
		DROP INDEX  `id_name_fk`;
		An alternative to temporarily disable all the foreign keys:

		SET FOREIGN_KEY_CHECKS=0;
		When you need to turn it on:

		SET FOREIGN_KEY_CHECKS=1;

#### Dump a Database:
###### Dump and rename:

	mysqldump -R old_db | mysql new_db

 	or just dump the database and import the file into a new database name:

	mysqldump -p -c -e TheNameOfTheDatabase > The_Name_of_the_Dump.sql

	To import from the MySQL command prompt type: source The_Name_of_the_Dump.sql

	or

	\. The_Name_of_the_Dump.sql

###### Dump a Table:

	mysqldump -p -c -e TheNameOfTheDatabase TheNameOfTheTable > The_Name_of_the_Dump.sql

###### Dump a single Database:

	mysqldump -p -c -e TheNameOfTheDatabase > The_Name_of_the_Dump.sql

###### Dump All Databases on the Server to a file:

	mysqldump -p -c -e --all-databases > The_Name_of_the_Dump.sql

###### Backup shell script to create a timestamped database dump:
```
    Script Name: dbdump.sh
    DBuser=SomeUser
    DBname=SomeDatabase
    TimeStamp=`date +"%Y%m%d%H%M%S%Z"`
    mysqldump -u$SomeUser -p -c -e $DBname > $TimeStamp.DBDump.$DBname.`hostname`.sql
    echo "Compressing Database Dump. Please wait..."
    tar -zcvf $TimeStamp.DBDump.$DBname.`hostname`.sql.gz $TimeStamp.DBDump.$DBname.`hostname`.sql
```

#### Duplicate Data:
###### Find duplicate data in a column.

		SELECT column1, COUNT(*) c FROM tablename GROUP BY column1 HAVING c > 1;

#### Enable remote connections for a specific IP address:
###### Create a database, create database user, and enable remote connections for that user from a specific IP address.
    -- Example:
    /*
        DB_NAME = webdb
        USER_NAME = webdb_user
        REMOTE_IP = 10.0.15.25
        PASSWORD = password123
        PERMISSIONS = ALL
    */

    -- CREATE DATABASE ##
    -- MariaDB [(none)]>
    	CREATE DATABASE webdb;

    -- CREATE USER ##
    -- MariaDB [(none)]>
    	CREATE USER 'webdb_user'@'10.0.15.25' IDENTIFIED BY 'password123';

    -- GRANT PERMISSIONS ##
    -- MariaDB [(none)]>
    	GRANT ALL ON webdb.* TO 'webdb_user'@'10.0.15.25';

    -- FLUSH PRIVILEGES, Tell the server to reload the grant tables  ##
    -- MariaDB [(none)]>
    	FLUSH PRIVILEGES;

#### ENUM:
###### Definition:
  ENUM is a good choice for boolean type of fields except that it is treated as a string
  and not an integer. In this case I just want to set a column in the table to indicate
  whether the row is active (1) or not (0). I do not want someone to accidentally enter
  a 2, 3, etc. in the field.

    Source: http://komlenic.com/244/8-reasons-why-mysqls-enum-data-type-is-evil/

    alter table healthtemperature1 add column active_ind enum('0','1') not null;

#### Event:
###### Creating Events:
http://stackoverflow.com/questions/10314806/mysql-triggers-deleting-a-row-after-inactivity
First, do not put this update/delete in a trigger, you are going to see a huge performance hit if there are millions of rows.
Instead, you can create a cron job or if you want to keep it all in MySQL use the MySQL Event scheduler.

Go to this page to read more about scheduling events in MySQL: http://dev.mysql.com/doc/refman/5.1/en/events.html

MySQL Event allows you to schedule things on MySQL on a regular basis.

The code would look something like:
```
    CREATE EVENT myevent
    ON SCHEDULE AT CURRENT_TIMESTAMP + INTERVAL 1 HOUR
    DO
    DELETE FROM MyTable Where Expired< NOW();
```
Example updates the state column to 1 if it is older than 24 hours.
```
	Check a table every hour and update a column that is 24 hours old:
    CREATE EVENT reset
        ON SCHEDULE
          EVERY 1 HOUR
            DO
    update T1
    set state=1
    where time < date_sub(now(),interval 24 hour)
      and (state=0 or state=2) ;
```
```
    CREATE EVENT reset ON SCHEDULE EVERY 1 HOUR DO update test set state=1 where time < date_sub(now(),interval 24 hour) and (state=0 or state=2);
```
Create Event Source: https://dba.stackexchange.com/questions/56424/column-auto-updated-after-24-hours-in-mysql


#### Foreign Keys:
###### Add foreign key constraint:

		alter table TableName
    	add constraint TheConstraintName
    	foreign key (CurrentTableColumnName) references ForeignTable(ColumnName)
    	on update cascade on delete restrict;

    	*If you do not give the constraint a name, then one will be automatically generated.
    	*Sometimes you will see a message "Check DataType" if the two columns are not exactly the same or there is a duplicate constraint name.

    Casecade only works if foreign_key_checks is ON. To see this information type:
    	show variables like 'foreign_key_checks';

    	If you want to see all variables type:
    	show variables;



###### Display Foreign Key References:
    -- To run from the command prompt type:
    -- mysql -u rob -p < display_foreign_key_references.sql > current_fk_refs.txt

####### Show constraints for all databases on the server:
    use INFORMATION_SCHEMA;
	select concat(`kcu`.`TABLE_SCHEMA`,'.',`kcu`.`TABLE_NAME`,'.',`kcu`.`COLUMN_NAME`) AS `This_DB_Table_and_Column`
	,concat(`kcu`.`TABLE_SCHEMA`,'.',`kcu`.`REFERENCED_TABLE_NAME`,'.',`kcu`.`REFERENCED_COLUMN_NAME`) AS `References_This_DB_Table_and_Column`
	,`kcu`.`CONSTRAINT_NAME` AS `CONSTRAINT_NAME`
	,`rc`.`UPDATE_RULE` AS `update_rule`
	,`rc`.`DELETE_RULE` AS `delete_rule`
	from (`information_schema`.`KEY_COLUMN_USAGE` `kcu`
	join `information_schema`.`referential_constraints` `rc` on(`kcu`.`TABLE_NAME` = `rc`.`TABLE_NAME`))
	where `kcu`.`REFERENCED_TABLE_NAME` is not null
	order by concat(`kcu`.`TABLE_SCHEMA`,'.',`kcu`.`TABLE_NAME`,'.',`kcu`.`COLUMN_NAME`);

####### Show constraints for specific database:
    use INFORMATION_SCHEMA;
    select distinct concat(`kcu`.`TABLE_SCHEMA`,'.',`kcu`.`TABLE_NAME`,'.',`kcu`.`COLUMN_NAME`) AS `This_DB_Table_and_column`
    ,concat(`kcu`.`TABLE_SCHEMA`,'.',`kcu`.`REFERENCED_TABLE_NAME`,'.',`kcu`.`REFERENCED_COLUMN_NAME`) AS `References_This_DB_Table_and_Column`
    ,`kcu`.`CONSTRAINT_NAME` AS `constraint_name`
    ,`rc`.`UPDATE_RULE` AS `update_rule`
    ,`rc`.`DELETE_RULE` AS `delete_rule`
    from (`information_schema`.`KEY_COLUMN_USAGE` `kcu`
    join `information_schema`.`REFERENTIAL_CONSTRAINTS` `rc` on(`kcu`.`TABLE_NAME` = `rc`.`TABLE_NAME`))
    where `kcu`.`REFERENCED_TABLE_NAME` is not null
    and `kcu`.`TABLE_SCHEMA` = 'YOURDATABASENAME'
    order by This_DB_Table_and_column;

####### Show constraints for all databases:
    create VIEW `vw_fk_global_constraints` AS
    select distinct concat(`kcu`.`TABLE_SCHEMA`,'.',`kcu`.`TABLE_NAME`,'.',`kcu`.`COLUMN_NAME`) AS `This_DB_Table_and_Column`
    ,concat(`kcu`.`TABLE_SCHEMA`,'.',`kcu`.`REFERENCED_TABLE_NAME`,'.',`kcu`.`REFERENCED_COLUMN_NAME`) AS `References_This_DB_Table_and_Column`
    ,`kcu`.`CONSTRAINT_NAME` AS `CONSTRAINT_NAME`
    ,`rc`.`UPDATE_RULE` AS `update_rule`
    ,`rc`.`DELETE_RULE` AS `delete_rule`
    from (
	`information_schema`.`KEY_COLUMN_USAGE` `kcu`
	join `information_schema`.`referential_constraints` `rc`
	on(`kcu`.`TABLE_NAME` = `rc`.`TABLE_NAME`))
	where `kcu`.`REFERENCED_TABLE_NAME` is not null
	order by concat(`kcu`.`TABLE_SCHEMA`,'.',`kcu`.`TABLE_NAME`,'.',`kcu`.`COLUMN_NAME`
    );

    -- This is a quick way to view all of the constraints:
    SELECT * FROM information_schema.REFERENTIAL_CONSTRAINTS;

    -- This is a quick way to view constraints from a specific database:
    select * from information_schema.referential_constraints where constraint_schema = 'thedatabasename';

Source: https://www.youtube.com/watch?v=UQK9_gKQHZg
####Generated Columns
    The syntax for defining a generated column is as follows:

       column_name data_type [GENERATED ALWAYS] AS (expression)
          [VIRTUAL | STORED] [UNIQUE [KEY]]

First, specify the column name and its data type.

Next, add the GENERATED ALWAYS clause to indicate that the column is a generated column.

Then, indicate whether the type of the generated column by using the corresponding option: VIRTUAL or STORED. By default, MySQL uses VIRTUAL if you dont specify explicitly the type of the generated column.

After that, specify the expression within the braces after the AS keyword. The expression can contain literals, built-in functions with no parameters, operators, or references to any column within the same table. If you use a function, it must be scalar and deterministic.

Finally, if the generated column is stored, you can define a unique constraint for it.

Generated column:
Columns are generated because the data in these columns are computed based on predefined expressions. Basically, the columns are generated on the fly based on the data that already exists in the table.

  Virtual Column:
  The "fullname" column is Virtual by default because the generated column type was not specified.

    DROP TABLE IF EXISTS contacts;
    CREATE TABLE contacts (
        id INT AUTO_INCREMENT PRIMARY KEY,
        first_name VARCHAR(50) NOT NULL,
        last_name VARCHAR(50) NOT NULL,
        fullname varchar(101) GENERATED ALWAYS AS (CONCAT(first_name,' ',last_name)),
        email VARCHAR(100) NOT NULL
    );

  MySQL provides two types of generated columns: stored and virtual. The virtual columns are calculated on the fly each time data is read whereas the stored column are calculated and stored physically when the data is updated.

  Based on this definition, the fullname column in the example above is a virtual column.

  Stored Column: (If the generated column is stored, you can define a unique constraint for it.)

    ALTER TABLE products ADD COLUMN stockValue DOUBLE GENERATED ALWAYS AS (buyprice*quantityinstock) STORED;

#### Grant:
###### Grant privileges.
    grant all on *.* to 'rob'@'localhost';

    show grants for 'root'@'localhost';
    show grants for 'rob'@'localhost';

    MySQL 8.0.X.X. Grant superuser privileges:
    use mysql;
    UPDATE `user` SET `Select_priv` = 'Y', `Insert_priv` = 'Y', `Update_priv` = 'Y', `Delete_priv` = 'Y', `Create_priv` = 'Y', `Drop_priv` = 'Y', `Reload_priv` = 'Y', `Shutdown_priv` = 'Y', `Process_priv` = 'Y', `File_priv` = 'Y', `Grant_priv` = 'Y', `References_priv` = 'Y', `Index_priv` = 'Y', `Alter_priv` = 'Y', `Show_db_priv` = 'Y', `Super_priv` = 'Y', `Create_tmp_table_priv` = 'Y', `Lock_tables_priv` = 'Y', `Execute_priv` = 'Y', `Repl_slave_priv` = 'Y', `Repl_client_priv` = 'Y', `Create_view_priv` = 'Y', `Show_view_priv` = 'Y', `Create_routine_priv` = 'Y', `Alter_routine_priv` = 'Y', `Create_user_priv` = 'Y', `Event_priv` = 'Y', `Trigger_priv` = 'Y', `Create_tablespace_priv` = 'Y', `Create_role_priv` = 'Y', `Drop_role_priv` = 'Y' WHERE `user`.`Host` = '%' AND `user`.`User` = 'rob';

    https://lefred.be/content/how-to-grant-privileges-to-users-in-mysql-8-0/
    Grant Privileges for a user to a database;
    grant alter,create,delete,drop,index,insert,select,update,trigger,alter routine,
    create routine, execute, create temporary tables on user1.* to 'user1';

    grant alter,create,delete,drop,index,insert,select,update,trigger,alter routine,
    create routine, execute, create temporary tables on hillc1.* to 'theusername';

    grant all privileges on thedatabasename.* to 'theusername'@'localhost' with grant option; flush privileges;
    grant all privileges on thedatabasename.* to 'theusername'@'%' with grant option; flush privileges;
    grant SELECT, INSERT, UPDATE, DELETE ON SomeDatabase TO 'theusername'@'localhost';

#### Group By: (Uses "Having" instead of "Where" clause.)
###### Find duplicate data in a column.

    SELECT column1, COUNT(*) c FROM tablename GROUP BY column1 HAVING c > 1;

###### Show number of presidents from each state.
    select state_born State, count(*) Number_of_Presidents from uspresidents group by state having Number_of_Presidents > 0 order by Number_of_Presidents, state;

#### IF and CASE Statements:
###### Select If:
There are times where running IF statements inside a query can be useful. MySQL provides a simple way to do this through the use of IF and CASE statements.

The IF statement takes three arguments; the conditional, the true value, and the false value. False and true values may be static values or column values. For example:

		SELECT IF(score >= 100, "Good Job", score) AS score FROM exam_results;

this will check if the value in the score column is 100 then print "Good Job" otherwise print the value of score. IF statements can also be nested:

		SELECT IF(score >= 100, "Good Job", IF(score < 100, "You Failed!", score)) score FROM exam_results;

###### CASE statements (switch statements for those C programmers) are much like if statements. For example:

    CREATE TABLE `headcount` (
      `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
      `num_heads` int(11) NOT NULL,
      `active_ind` int(1) NOT NULL DEFAULT '1',
      PRIMARY KEY (`id`)
    ) ENGINE=InnoDB;

    SELECT CASE num_heads
    WHEN 0 THEN 'Zombie'
    WHEN 1 THEN 'Human'
    ELSE 'Alien'
    END AS race
    FROM headcount;

This code checks the value in the num_heads column and deduces race from the values presented. CASE statements may also be nested in the same way as IF statements.

I used this to prepend a zero in front of values that were less than 10.

		select concat("update yt_video_rename set day = ",if(day<10, concat("0",day),day)," where id = ", id,";") xyz from yt_video_rename order by day;

Count the number of presidents from each party:

		select sum(if(party = 1, 1,0)) as Federalist, sum(if(party = 2, 1,0)) as "Democratic-Republican", sum(if(party = 3,1,0)) as Democrat, sum(if(party = 4,1,0)) as Whig, sum(if(party = 5,1,0)) Republican, sum(if(party = 6,1,0)) "Democratic-Union", sum(if(party = 7,1,0)) Republican1 from us_presidents;

		-- Start at 0 and increment by 1 for each party member found.

#### Increment results numerically (count results). Good for displaying first, second, third place:
    SELECT @n := @n + 1 "Item#:",
           firstname,
           lastname
      FROM test, (SELECT @n := 0) m
     ORDER BY firstname, lastname;

    My working example:
    select @n := @n + 1 place,
    	person, medication, dose_unit, admin_dttm, temp_f, temp_c, symptom
    from
    	vw_healthsummary, (select @n := 0) m
    order by temp_f desc limit 0, 50;


    Online Example for SQLServer:

    SELECT row_number() OVER (ORDER BY first_name, last_name) n,
           first_name,
           last_name
      FROM table1


    Source: https://stackoverflow.com/questions/16555454/how-to-generate-auto-increment-field-in-select-query

#### InnoDB vs MyISAM:

The main differences between InnoDB and MyISAM ("with respect to designing a table or database" you asked about) are support for "referential integrity" and "transactions".

If you need the database to enforce foreign key constraints, or you need the database to support transactions (i.e. changes made by two or more DML operations handled as single unit of work, with all of the changes either applied, or all the changes reverted) then you would choose the InnoDB engine, since these features are absent from the MyISAM engine.

Those are the two biggest differences. Another big difference is concurrency. With MyISAM, a DML statement will obtain an exclusive lock on the table, and while that lock is held, no other session can perform a SELECT or a DML operation on the table.

Those two specific engines you asked about (InnoDB and MyISAM) have different design goals. MySQL also has other storage engines, with their own design goals.

So, in choosing between InnoDB and MyISAM, the first step is in determining if you need the features provided by InnoDB. If not, then MyISAM is up for consideration.

A more detailed discussion of differences is rather impractical (in this forum) absent a more detailed discussion of the problem space... how the application will use the database, how many tables, size of the tables, the transaction load, volumes of select, insert, updates, concurrency requirements, replication features, etc.

The logical design of the database should be centered around data analysis and user requirements; the choice to use a relational database would come later, and even later would the the choice of MySQL as a relational database management system, and then the selection of a storage engine for each table.

###### MYISAM:

MYISAM supports Table-level Locking
MyISAM designed for need of speed
MyISAM does not support foreign keys hence we call MySQL with MYISAM is DBMS
MyISAM stores its tables, data and indexes in diskspace using separate three different files. (tablename.FRM, tablename.MYD, tablename.MYI)
MYISAM not supports transaction. You cannot commit and rollback with MYISAM. Once you issue a command its done.
MYISAM supports fulltext search
You can use MyISAM, if the table is more static with lots of select and less update and delete.

###### INNODB:

InnoDB supports Row-level Locking
InnoDB designed for maximum performance when processing high volume of data
InnoDB support foreign keys hence we call MySQL with InnoDB is RDBMS
InnoDB stores its tables and indexes in a tablespace
InnoDB supports transaction. You can commit and rollback with InnoDB

Source:
http://stackoverflow.com/questions/12614541/whats-the-difference-between-myisam-and-innodb

#### Insert Into:
###### INSERT INTO ANOTHER TABLE FROM CURRENT TABLE
First, make an empty version (copy) of a table by using CREATE TABLE.
Example:

		CREATE TABLE secondtable LIKE firsttable;

		-- This example inserts two columns into the secondtable table from the firsttable table.

		insert into secondtable (column1, column2) select column1, column2 from firsttable;

		-- Another method:
		CREATE TABLE secondtable AS
		SELECT columns
		FROM firsttable
		WHERE conditions;

#### INT vs BIGINT:
    -- http://stackoverflow.com/questions/3135804/types-in-mysql-bigint20-vs-int20-etcc

    INT is a four-byte signed integer. BIGINT is an eight-byte signed integer.

    The 20 in INT(20) and BIGINT(20) means almost nothing. It's a hint for display width, it has nothing to do with storage. Practically, it affects only the ZEROFILL option:

    CREATE TABLE foo ( bar INT(20) ZEROFILL );
    INSERT INTO foo (bar) VALUES (1234);
    SELECT bar from foo;

    +----------------------+
    | bar                  |
    +----------------------+
    | 00000000000000001234 |
    +----------------------+
    It's a common source of confusion for MySQL users to see INT(20) and assume it's a size limit, something analogous to CHAR(20).

#### Joins:
**<img src="../img/joins1_left1.png" /> Left Inner Join**<br />
**<img src="../img/joins2_left1.png" /> Left Join**<br />
**<img src="../img/joins3_inner1.png" />Inner Join**<br />
**<img src="../img/joins4_right1.png" />Right Inner Join**<br />
**<img src="../img/joins5_right1.png" />Right Join**<br />
**<img src="../img/joins6_full_outer1.png" />Full Outer Join**<br />
**<img src="../img/joins7_full_outer1.png" />Full Inner Join**<br />

###### Join with no where clause:
  I have two tables I want to join.

  I want all of the categories in the categories table and also all of the categories subscribed to by a user in the category_subscriptions table.

  essentially this is my query so far:

    SELECT *
    FROM categories
    LEFT JOIN user_category_subscriptions
    ON user_category_subscriptions.category_id = categories.category_id;

  This works fine however I want to add a where clause on the end of the query which then essentially makes it an inner/equi join.

    SELECT *
    FROM categories
    LEFT JOIN user_category_subscriptions
    ON user_category_subscriptions.category_id = categories.category_id
    WHERE user_category_subscriptions.user_id = 1;

  How do I get all the categories as well as all the categories subscribed to by a particular user using only one query?

  category_id being a key in both categories table and user_category_subscriptions. user_id residing in the user_category_subscriptions table.

  thanks

###### Join with no where clause ANSWER:

  You need to put it in the join clause, not the where:

    SELECT *
    FROM categories
    LEFT JOIN user_category_subscriptions ON
    user_category_subscriptions.category_id = categories.category_id
    and user_category_subscriptions.user_id =1;

  See, with an inner join, putting a clause in the join or the where is equivalent. However, with an outer join, they are vastly different.

  As a join condition, you specify the rowset that you will be joining to the table. This means that it evaluates user_id = 1 first, and takes the subset of user_category_subscriptions with a user_id of 1 to join to all of the rows in categories. This will give you all of the rows in categories, while only the categories that this particular user has subscribed to will have any information in the user_category_subscriptions columns. Of course, all other categories will be populated with null in the user_category_subscriptions columns.

  Conversely, a where clause does the join, and then reduces the rowset. So, this does all of the joins and then eliminates all rows where user_id doesn't equal 1. You're left with an inefficient way to get an inner join.

#### Last Insert ID:
###### Getting Last Insert ID:

    drop database lastinsert_id;
    create database lastinsert_id;
    use lastinsert_id;
    create table foo (id int(11) auto_increment primary key
    , text varchar(50) not null)engine=innodb;

    create table foo2 (id int(11) auto_increment primary key
    , foo_id int(11) not null, text varchar(50) not null)engine=innodb;


-- https://dev.mysql.com/doc/c-api/5.6/en/getting-unique-id.html

    INSERT INTO foo (id,text)
        VALUES(NULL,'filename');         # generate ID by inserting NULL
    INSERT INTO foo2 (id,foo_id,text)
        VALUES(NULL,LAST_INSERT_ID(),'last_insert_id.sql');  # use ID in second table


###### Last Insert ID Using PDO:
    -- https://stackoverflow.com/questions/10680943/pdo-get-the-last-id-inserted
    $stmt = $db->prepare("...");
    $stmt->execute();
    $id = $db->lastInsertId();
    If you want to do it with SQL instead of the PDO API, you would do it like a normal select query:

    $stmt = $db->query("SELECT LAST_INSERT_ID()");
    $lastId = $stmt->fetchColumn();


#### Load input (local_infile):
    insert into cv (id,content) values ("1",LOAD_FILE('cv.doc'));

    MySQL 8.0 has the load data local_infile option off by default. You can enable it by logging into the MySQL server and running:
    mysql> show global variables like 'local_infile';
    +---------------+-------+
    | Variable_name | Value |
    +---------------+-------+
    | local_infile  | OFF   |
    +---------------+-------+
    1 row in set (0.01 sec)

    mysql> set global local_infile = true;
    Query OK, 0 rows affected (0.00 sec)

    mysql> show global variables like 'local_infile';
    +---------------+-------+
    | Variable_name | Value |
    +---------------+-------+
    | local_infile  | ON    |
    +---------------+-------+
    1 row in set (0.00 sec)

    Afterward, you will have to start the MySQL client with:
    /usr/local/mysql/bin/mysql -u USERNAME -p --local-infile DATABASENAME
    mysql -u USERNAME -p --local-infile DATABASENAME
    Source: https://stackoverflow.com/questions/10762239/mysql-enable-load-data-local-infile

    -- From the MySQL command prompt.
    -- It is easier to have the file you want to import located in the same directory where you start mysql. Then run load data local infile once you log in.
    -- I loaded the exported Bedrock .csv files into a database using the following:

    /* The database and table.
    create database bedrock;
    use bedrock;
    if exist drop table bedrock_csv;
    create table bedrock_csv (id int(11) unsigned auto_increment primary key,
    audit_type varchar(500) null,
    topic_name varchar(500) null,
    filter_sequence varchar(500) null,
    filter_meaning varchar(500) null,
    filter_type_meaning varchar(500) null,
    filter_name varchar(500) null,
    flex_display varchar(500) null,
    saved_value varchar(500) null,
    description varchar(500) null,
    event_set_name varchar(500) null,
    code_value_id varchar(500) null,
    value_type varchar(500) null,
    value_sequence varchar(500) null,
    value_group_sequence varchar(500) null,
    qualifier varchar(500) null,
    map_type varchar(500) null,
    mapped_to_code_1 varchar(500) null,
    mapped_to_description_1 varchar(500) null,
    mapped_to_code_2 varchar(500) null,
    mapped_to_description_2 varchar(500) null,
    last_update_date_time varchar(500) null,
    last_update_by varchar(500) null
    ) engine=innodb;
    */

    -- I combined all of the exported Bedrock .csv files into one large file called allfiles.dat by using sed to remove the first header row.
    -- Example: sed '1d' Exported_CSV_FILE.csv >> allfiles.dat
    -- http://unix.stackexchange.com/questions/96226/delete-first-line-of-a-file

    load data local infile 'allfiles.dat' into table bedrock_csv fields terminated by ',' enclosed by '"' lines terminated by '\n' (audit_type, topic_name, filter_sequence, filter_meaning, filter_type_meaning, filter_name, flex_display, saved_value, description, event_set_name, code_value_id, value_type, value_sequence, value_group_sequence, qualifier,  map_type, mapped_to_code_1, mapped_to_description_1, mapped_to_code_2, mapped_to_description_2, last_update_date_time, last_update_by);

    load data infile 'allfiles.dat' replace into table bedrock_csv;

    -- Using the "local" keyword helped me get past the error message: "The MySQL server is running with the --secure-file-priv option so it cannot execute this statement".
    -- https://stackoverflow.com/questions/32737478/how-should-i-tackle-secure-file-priv-in-mysql
    load data local infile 'US_States.csv' into table us_states fields terminated by '|' lines terminated by '\n' (state,abbreviation,capital,largest_city,established,population,sq_mi,sq_km,land_area_mi,land_area_km,water_area_mi,water_area_km,representatives);

    /*Another example:
    I was stuck on a problem where the ImportXML3.xml file would not get imported into the database because
    the XML tag names were in different case on some of the lines. Once I made them the same case it was imported.
    --
    This online link was helpful. http://dev.mysql.com/doc/refman/5.5/en/load-xml.html
    This statement supports three different XML formats:

    Column names as attributes and column values as attribute values:
      <row column1="value1" column2="value2" .../>

    Column names as tags and column values as the content of these tags:
      <row>
        <column1>value1</column1>
        <column2>value2</column2>
        </row>

    Column names are the name attributes of <field> tags, and values are the contents of these tags:
      <row>
        <field name='column1'>value1</field>
        <field name='column2'>value2</field>
        </row>
    This is the format used by other MySQL tools, such as mysqldump.

    All three formats can be used in the same XML file; the import routine automatically detects the format for each row and interprets it correctly. Tags are matched based on the tag or attribute name and the column name.
    */

    LOAD XML LOCAL INFILE 'ImportXML3.xml'
    INTO TABLE xmlimport3
    ROWS IDENTIFIED BY '<myfields>';

    /*The ImportXML3.xml file looks like this:
    <rlh>
    <myfields><lastname>firstname01</lastname><firstname>lastname01</firstname></myfields>
    <myfields><lastname>firstname02</lastname><firstname>lastname02</firstname></myfields>
    <myfields><lastname>firstname03</lastname><firstname>lastname03</firstname></myfields>
    <myfields><lastname>firstname04</lastname><firstname>lastname04</firstname></myfields>
    <myfields><lastname>firstname05</lastname><firstname>lastname05</firstname></myfields>
    <myfields><lastname>firstname06</lastname><firstname>lastname06</firstname></myfields>
    <myfields><lastname>firstname07</lastname><firstname>lastname07</firstname></myfields>
    <myfields><lastname>firstname08</lastname><firstname>lastname08</firstname></myfields>
    <myfields><lastname>firstname09</lastname><firstname>lastname09</firstname></myfields>
    <myfields><lastname>firstname10</lastname><firstname>lastname10</firstname></myfields>
    <myfields><lastname>firstname11</lastname><firstname>lastname11</firstname></myfields>
    <myfields><lastname>firstname12</lastname><firstname>lastname12</firstname></myfields>
    <myfields><lastname>firstname13</lastname><firstname>lastname13</firstname></myfields>
    <myfields><lastname>firstname14</lastname><firstname>lastname14</firstname></myfields>
    <myfields><lastname>firstname15</lastname><firstname>lastname15</firstname></myfields>
    <myfields><lastname>firstname16</lastname><firstname>lastname16</firstname></myfields>
    <myfields><lastname>firstname17</lastname><firstname>lastname17</firstname></myfields>
    </rlh>
    */

    I got an error when I tried to load some data exported from an Excel spreadsheet in .csv format. The error message was "ERROR 1300 (HY000): Invalid utf8mb4 character string:"

    I wasn't able to manually correct all of the invalid characters in the .csv file because there were too many. There is a command on Linux called "file" that will tell you the file type. When I ran it "file -i filename.csv" it displayed a message telling me unknown.

    file -i mpages1.csv

    I found a website that suggested that the file might be latin so I used another Linux command called "iconv" to convert it from latin to UTF8 and I was able to import the .csv into MySQL.

    iconv -f latin1 -t utf8 < mpages1.csv > mpages2.csv
    This worked: (Source: https://unix.stackexchange.com/questions/141539/iconv-illegal-input-sequence-why).

#### Change database and table collation and char set to utf8mb4 and utf8mb4_unicode_ci.:

    ALTER DATABASE <db_name> CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    ALTER TABLE <table_name> CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    (Source: https://stackoverflow.com/questions/48270374/invalid-datetime-format-1366-incorrect-string-value)

#### Locate MySQL Database Files:
Typically the MySQL database files are located in /usr/local/mysql/data/databasename/

    select @@datadir, @@innodb_data_home_dir;

###### File locations:
    SELECT TABLESPACE_NAME, FILE_NAME FROM INFORMATION_SCHEMA.FILES \G

#### Natural Sorting of Numbers:
	https://stackoverflow.com/questions/8557172/mysql-order-by-sorting-alphanumeric-correctly
	https://www.copterlabs.com/natural-sorting-in-mysql/

    select lastname, firstname, salary, jobtitle, hiredate from payback order by cast(salary as unsigned), salary;

#### Output to a file:

###### From the mysql command prompt:
```
You can create an output file formatted with comma delimiters and fields enclosed by quotes. The mysql user must have privileges to the output file location.
select * into
outfile 'outputfilename.txt'
fields terminated by ','
optionally enclosed by '"'
lines terminated by '\n'
from yourtablename
where columnname = 'whatever';

If no path is specified, the file will be located in the default database folder. In my case (Fedora 12) it was located in /var/lib/mysql/thedatabasename/outputfilename.txt.
```
```
-- You can specify where the output file will go:
SELECT id,
   client,
   project,
   task,
   description,
   time,
   date
  INTO OUTFILE '/path/to/file.csv' --mysql user must have privileges to the location.
  FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
  LINES TERMINATED BY '\n'
  FROM ts
```

From outside of the mysql command prompt (ie. the command line) you can also run a query and create an output file with the results of that query. Create a query that you want to run and save it as an .sql file. Example: test.sql

```
The content of the test.sql file looks like this:
				select * from tablename;
```

To run test.sql type one of the following:

-- If you want tab delimited output format (default):
```
mysql databasename -u username -p < test.sql > output.tab

Convert the tabs to comma delimited surrounded by quotes:
mysql -u username -p -h computername.lan < test.sql |sed 's/\t/\",\"/g'|sed 's/^/\"/g'|sed 's/$/\"/g' > output.csv
```
-- XML output format:
```
mysql databasename -u username -p --xml < test.sql > output.xml
```
-- If you don't want to create the test.sql file and just want to run everything from one commandline statement and get XML output:
```
mysql -u username -p --xml -e 'use databasename; select * from tablename' > output.xml
```
-- You can also put the db_name in your script to avoid typing it on the command line (see below).
```
mysql -u username -p --xml < test.sql > output.xml
```
-- You can create a bash script named getdata and put the following in it.
```
mysql -u username -p < test.sql > test.tab

-- Then chmod +x getdata. then run it from the commandline: sh getdata.
-- You will be prompted for your database password and the data will get dumped to test.tab.
```

-- The contents of test.sql without the database name.
```
select * from tablename order by columnName;
```
-- The contents of test.sql with the database name.
```
use thedatabase;
select * from tablename order by columnName;
```

-- Connect to a remote database server and directly to a database on that server.
```
mysql -h hostname -u databaseuser -p -D databasename
```

-- To Dump a database to a file and generate full insert statements:
```
mysqldump -p -c -e databasename > DatabaseName.sql
```

-- To Dump the database data without the database structure:
```
mysqldump -u root -p thedatabasename --no-create-info > 20240609.sql
```

-- To dump a table from a database and generate full insert statements:
```
mysqldump -p -c -e databasename tablename > TableName.sql
```

-- To dump multiple tables from a database:
```
mysqldump -u theusername -p thedatabasename tablename1 tablename1 tablename2 tablename3 tablename4 tablename5 > thedate_thedatabasename_tables_on_`hostname`.sql
```

-- To dump all databases on the database server:
```
mysqldump -p -c -e --all-databases > AllDatabases.sql
```

-- To dump all databases on the database server without the data (just a skeleton).
```
mysqldump -p -c -e --no-data --all-databases > AllDatabases_Skeleton.sql
```

-- To dump a database from a remote server:
```
mysqldump -h hostname -u username -p -c -e databasename > NameOfDatabaseDumpFile.sql
```

-- To dump a table from a database on a remote server:
```
mysqldump -h hostname -u username -p -c -e databasename tablename > NameOfTableDumpFile.sql
```

-- To dump all databases on a remote server:
```
mysqldump -h hostname -u username -p -c -e --all-databases > NameOfEntireDatabaseDumpFile.sql
```

-- Restore database from a file:
```
mysql -u root -p thedatabasename < 20200424_thedatabasename.sql
```

#### Padding numbers with zeros:
###### Number padding
    -- Prepend zeros to numbers. There are some links that I saw that said you will need to convert the column to non-numerical to get this to work but I did it on an integer field and it worked.

    -- The 8 means to pad up to 8 characters, the zero is the character you want to pad with.
    SELECT LPAD('1234567', 8, '0');

#### Password Change:

    use mysql;
    -- Method 1 (Deprecated):
    update mysql.user set password('thepassword') where user = 'root';
    FLUSH PRIVILEGES;

    -- Method 2 (MySQL 5.7+):
    update mysql.user set authentication_string=PASSWORD('thepassword') where user='root';
    FLUSH PRIVILEGES;

    -- Method 3 (Preferred method for current user.):
    alter user set password = 'thepassword';
    FLUSH PRIVILEGES;

    -- MySQL 5.7:
    alter user 'root'@'localhost' identified by 'thepassword';
    alter user 'root'@'%' identified by 'thepassword';

    -- Method 4 (Preferred method for another user.):
    alter user set password for 'root'@'localhost' = 'thepassword';
    FLUSH PRIVILEGES;

    -- Remote user password change:
    alter user set password for 'root'@'%' = 'thepassword';
    FLUSH PRIVILEGES;

#### Path to MySQL files:
    On my MAC:
    MySQL program:
      /usr/local/mysql/bin/mysql

    Databases:
      /usr/local/mysql/data/

    On Ubuntu:
    MySQL program:
      /usr/bin/mysql

    Databases (need to be root):
      /var/lib/mysql/


#### Prompt (MySQL):
Change the default mysql> prompt to something functional and useful.

	1. Display username, hostname and current database name in the mysql prompt

    The MYSQL_PS1 in this example displays the following three information in the prompt:
```
    \u - Username
    \h - Hostname
    \d - Current mysql database

    $ export MYSQL_PS1="\u@\h [\d]> "

    $ mysql -u root -pyour-password -D sugarcrm

    root@dev-db [sugarcrm]>
```
	2. Change the mysql> prompt interactively

    You can also change the mysql> prompt interactively from inside the mysql as shown below.
```
    $ mysql -u root -pyour-password -D sugarcrm

    mysql> prompt \u@\h [\d]>
    PROMPT set to '\u@\h [\d]> '

    root@dev-db [sugarcrm]>
```
	3. Change the mysql> prompt from mysql command line

    Instead of using the MYSQL_PS1 variable, you can also pass the prompt as an argument to the mysql command line as shown below.
```
    $ mysql --prompt="\u@\h [\d]> " -u root -pyour-password -D sugarcrm

    root@dev-db [sugarcrm]>
```
	4. Display Current Time in the mysql> prompt

    Use \D to display full date in the mysql prompt as shown below.
```
    $ export MYSQL_PS1="\u@\h [\D]> "

    $ mysql -u root -pyour-password -D sugarcrm

    root@dev-db [Sat Dec 26 19:56:33 2009]>
```
	5. Change the mysql> prompt using /etc/my.cnf or .my.cnf file

    You can also use either the global /etc/my.cnf (or) your local ~/.my.cnf file to set the prompt as shown below.
```
    $ vi ~/.my.cnf

    [mysql]
    prompt=\\u@\\h [\\d]>\\_

    $ mysql -u root -pyour-password -D sugarcrm

    root@dev-db [sugarcrm]>
```
	6. Customize mysql> prompt any way you want it

    Use the following variables and customize the mysql prompt as you see fit. These variables are somewhat similar to the Unix PS1 variables (but not exactly the same).
```
    Generic variables:

    \S displays semicolon
    \' displays single quote
    \" displays double quote
    \v displays server version
    \p displays port
    \\ displays backslash
    \n displays newline
    \t displays tab
    \ displays space (there is a space after \ )
    \d displays default database
    \h displays default host
    \_ displays space (there is a underscore after \ )
    \c displays a mysql statement counter. keeps increasing as you type commands.
    \u displays username
    \U displays username@hostname accountname
    Date related variables:

    \D displays full current date (as shown in the above example)
    \w displays 3 letter day of the week (e.g. Mon)
    \y displays the two digit year
    \Y displays the four digit year
    \o displays month in number
    \O displays 3 letter month (e.g. Jan)
    \R displays current time in 24 HR format
    \r displays current time in 12 hour format
    \m displays the minutes
    \s displays the seconds
    \P displays AM or PM
    Note: You can go back to the regular boring mysql> prompt at anytime by simply typing prompt in the mysql> prompt as shown below.

    root@dev-db [sugarcrm]> prompt
    Returning to default PROMPT of mysql>
    mysql>


    <a href='http://www.thegeekstuff.com/2010/02/mysql_ps1-6-examples-to-make-your-mysql-prompt-like-angelina-jolie/'>Source</a>

    mysql -h localhost -u rob_com1 -p -D robcom1
```
#### Remote connection from commandline:
###### You should only use this command on a secure SSH connection.

    Syntax:
  	mysql -h RemoteServerName -u myusername -p

  	Connect to a remote database server and directly to a database on that server.
		mysql -h hostname -u databaseuser -p -D databasename

#### Rename a Database
    The normal way to rename a database is to dump it then import the data to a new database name. Make sure you check the definer for any views that were created in the database.

    To rename a table type:
    	RENAME TABLE tb1 TO tb2;

    Another way to rename a table;
    ALTER TABLE exampletable RENAME TO new_table_name;

    The commands below are what I copied from a Stack Exchange article but they did not work for me. I am only leaving them here so that I can study them at some other time.

    /*
    mysql -e "CREATE DATABASE \`new_database\`;"
    for table in `mysql -B -N -e "SHOW TABLES;" old_database`
    do
      mysql -e "RENAME TABLE \`old_database\`.\`$table\` to \`new_database\`.\`$table\`"
    done
    mysql -e "DROP DATABASE \`old_database\`;"
    */
    mysql -u robertme -p
    mysql -e "CREATE DATABASE \`united_states\`;"
    for table in `mysql -B -N -e "SHOW TABLES;" test`
    do
      mysql -e "RENAME TABLE \`test\`.\`$table\` to \`united_states\`.\`$table\`"
    done
    mysql -e "DROP DATABASE \`test\`;"

#### Revoke:
		https://mariadb.com/kb/en/revoke/
		https://www.techonthenet.com/mariadb/grant_revoke.php
		revoke all privileges, grant option from 'SomeUser'@'%';
		revoke all privileges, grant option from 'SomeUser'@'localhost';
		revoke SELECT, INSERT, UPDATE, DELETE ON SomeDatabase TO 'SomeUser'@'localhost';

#### Select:
###### Select across databases;
		select mysql.user.user from mysql.user;

		-- Example on https://stackoverflow.com/questions/674115/select-columns-across-different-databases
		SELECT
    	mydatabase1.tblUsers.UserID,
    	mydatabse2.tblUsers.UserID
		FROM
   		mydatabase1.tblUsers
		INNER JOIN mydatabase2.tblUsers
		ON mydatabase1.tblUsers.UserID = mydatabase2.tblUsers.UserID

###### Select Blobdata:
		SELECT SUBSTRING(<BLOB COLUMN_NAME>,1,2500) FROM <Table_name>;

###### Select current user:
		SELECT current_user();

###### Select data from the commandline:
		mysql -uusername -p -e"select current_user();"
		mysql -uusername -p -e"select user from mysql.user;"

###### Null and Not NULL:
    Show what IS NOT NULL:
    SELECT *
    FROM table
    WHERE YourColumn IS NOT NULL;

    This seems to show what IS NULL:
    SELECT *
    FROM table
    WHERE NOT (YourColumn <=> NULL);

    http://stackoverflow.com/questions/5285448/mysql-select-only-not-null-values

#### Shell Commands:
If you want to run shell commands from within the MySQL command prompt use a backslash and exclaimation mark:

	Example:
	\! ls -al

#### Show columns/tables/databases:
```
	To show columns:
		show columns from <table> from <database>;
			or (if you are already in the database)
		desc <table>;
```

```
	To show tables:
		show tables from <database>;
			or (if you are already in the database)
		show tables;
```

```
	To show databases:
		show databases;
			or (if you are already in the database)
		show schemas;
```

```
	To show database file location:
		show variables where Variable_name like '%datadir%';
```

```
	To show grants for a particular user:
		show grants for root@localhost
```

#### Service (MySQL):
###### Linux and/or MAC:
```
    Restart, Start, Stop MySQL from the Command Line macOS, OSX, Linux
    November 19, 2015 24 Comments
    To restart, start or stop MySQL server from the command line, type the following at the shell prompt

    On Linux start/stop/restart from the command line:
     /etc/init.d/mysqld start
     /etc/init.d/mysqld stop
     /etc/init.d/mysqld restart
    Some Linux flavors offer the service command too

     service mysqld start
     service mysqld stop
     service mysqld restart
    or

     service mysql start
     service mysql stop
     service mysql restart

    On macOS Sierra & OS to start/stop/restart MySQL post 5.7  from the command line:
    Start:
    sudo launchctl load -F /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist
    Stop:
    sudo launchctl unload -F /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist

    On OS X to start/stop/restart MySQL pre 5.7  from the command line:
     sudo /usr/local/mysql/support-files/mysql.server start
     sudo /usr/local/mysql/support-files/mysql.server stop
     sudo /usr/local/mysql/support-files/mysql.server restart

```

####Source:
Use "source" to run a query from outside the database command prompt window. Example: if you have a query file
named "bigdata.sql" that contains valid MySQL statements that you want to run.

		Example:
		source bigdata.sql;

		or

		\. bigdata.sql

####Flush Privileges Error:
    ERROR 1227 (42000): Access denied; you need (at least one of) the RELOAD privilege(s) for this operation
    Solution:  GRANT RELOAD ON *.* TO 'your_user'@'localhost';
    GRANT RELOAD ON *.* TO 'rob'@'localhost';
    GRANT RELOAD ON *.* TO 'rob'@'%';

#### Statements and Clauses (MySQL):
###### MYSQL Statements and clauses

  ALTER DATABASE

  ALTER TABLE

  ALTER VIEW

  ANALYZE TABLE

  BACKUP TABLE

  CACHE INDEX

  CHANGE MASTER TO

  CHECK TABLE

  CHECKSUM TABLE

  COMMIT

  CREATE DATABASE

  CREATE INDEX

  CREATE TABLE

  CREATE VIEW

  DELETE

  DESCRIBE

  DO

  DROP DATABASE

  DROP INDEX

  DROP TABLE

  DROP USER

  DROP VIEW

  EXPLAIN

  FLUSH

  GRANT

  HANDLER

  INSERT

  JOIN

  KILL

  LOAD DATA FROM MASTER

  LOAD DATA INFILE

  LOAD INDEX INTO CACHE

  LOAD TABLE...FROM MASTER

  LOCK TABLES

  OPTIMIZE TABLE

  PURGE MASTER LOGS

  RENAME TABLE

  REPAIR TABLE

  REPLACE

  RESET

  RESET MASTER

  RESET SLAVE

  RESTORE TABLE

  REVOKE

  ROLLBACK

  ROLLBACK TO SAVEPOINT

  SAVEPOINT

  SELECT

  SET

  SET PASSWORD

  SET SQL_LOG_BIN

  SET TRANSACTION

  SHOW BINLOG EVENTS

  SHOW CHARACTER SET

  SHOW COLLATION

  SHOW COLUMNS

  SHOW CREATE DATABASE

  SHOW CREATE TABLE

  SHOW CREATE VIEW

  SHOW DATABASES

  SHOW ENGINES

  SHOW ERRORS

  SHOW GRANTS

  SHOW INDEX

  SHOW INNODB STATUS

  SHOW LOGS

  SHOW MASTER LOGS

  SHOW MASTER STATUS

  SHOW PRIVILEGES

  SHOW PROCESSLIST

  SHOW SLAVE HOSTS

  SHOW SLAVE STATUS

  SHOW STATUS

  SHOW TABLE STATUS

  SHOW TABLES

	show tables like 'abc%';

  SHOW VARIABLES

  SHOW WARNINGS

  START SLAVE

  START TRANSACTION

  STOP SLAVE

  TRUNCATE TABLE

  UNION

  UNLOCK TABLES

  USE

###### String Functions


  AES_DECRYPT

  AES_ENCRYPT

  ASCII

  BIN

  BINARY

  BIT_LENGTH

  CHAR

  CHAR_LENGTH

  CHARACTER_LENGTH

  COMPRESS

  CONCAT

  CONCAT_WS

  CONV

  DECODE

  DES_DECRYPT

  DES_ENCRYPT

  ELT

  ENCODE

  ENCRYPT

  EXPORT_SET

  FIELD

  FIND_IN_SET

  HEX

  INET_ATON

  INET_NTOA

  INSERT

  INSTR

  LCASE

  LEFT

  LENGTH

  LOAD_FILE

  LOCATE

  LOWER

  LPAD

  LTRIM

  MAKE_SET

  MATCH    AGAINST

  MD5

  MID

  OCT

  OCTET_LENGTH

  OLD_PASSWORD

  ORD

  PASSWORD

  POSITION

  QUOTE

  REPEAT

  REPLACE

  REVERSE

  RIGHT

  RPAD

  RTRIM

  SHA

  SHA1

  SOUNDEX

  SPACE

  STRCMP

  SUBSTRING

  SUBSTRING_INDEX

  TRIM

  UCASE

  UNCOMPRESS

  UNCOMPRESSED_LENGTH

  UNHEX

  UPPER

###### Date and Time Functions

  ADDDATE

  ADDTIME

  CONVERT_TZ

  CURDATE

  CURRENT_DATE

  CURRENT_TIME

  CURRENT_TIMESTAMP

  CURTIME

  DATE

  DATE_ADD

  DATE_FORMAT

  DATE_SUB

  DATEDIFF

  DAY

  DAYNAME

  DAYOFMONTH

  DAYOFWEEK

  DAYOFYEAR

  EXTRACT

  FROM_DAYS

  FROM_UNIXTIME

  GET_FORMAT

  HOUR

  LAST_DAY

  LOCALTIME

  LOCALTIMESTAMP

  MAKEDATE

  MAKETIME

  MICROSECOND

  MINUTE

  MONTH

  MONTHNAME

  NOW

  PERIOD_ADD

  PERIOD_DIFF

  QUARTER

  SEC_TO_TIME

  SECOND

  STR_TO_DATE

  SUBDATE

  SUBTIME

  SYSDATE

  TIME

  TIMEDIFF

  TIMESTAMP

  TIMESTAMPDIFF

  TIMESTAMPADD

  TIME_FORMAT

  TIME_TO_SEC

  TO_DAYS

  UNIX_TIMESTAMP

  UTC_DATE

  UTC_TIME

  UTC_TIMESTAMP

  WEEK

  WEEKDAY

  WEEKOFYEAR

  YEAR

  YEARWEEK

###### Mathematical and Aggregate Functions


  ABS

  ACOS

  ASIN

  ATAN

  ATAN2

  AVG

  BIT_AND

  BIT_OR

  BIT_XOR

  CEIL

  CEILING

  COS

  COT

  COUNT

  CRC32

  DEGREES

  EXP

  FLOOR

  FORMAT

  GREATEST

  GROUP_CONCAT

  LEAST

  LN

  LOG

  LOG2

  LOG10

  MAX

  MIN

  MOD

  PI

  POW

  POWER

  RADIANS

  RAND

  ROUND

  SIGN

  SIN

  SQRT

  STD

  STDDEV

  SUM

  TAN

  TRUNCATE

  VARIANCE

###### Flow Control Functions


  CASE

  IF

  IFNULL

  NULLIF

###### Command-Line Utilities


  comp_err

  isamchk

  make_binary_distribution

  msql2mysql

  my_print_defaults

  myisamchk

  myisamlog

  myisampack

  mysqlaccess

  mysqladmin

  mysqlbinlog

  mysqlbug

  mysqlcheck

  mysqldump

  mysqldumpslow

  mysqlhotcopy

  mysqlimport

  mysqlshow

  perror

###### Perl API - using functions and methods built into the Perl DBI with MySQL


  available_drivers

  begin_work

  bind_col

  bind_columns

  bind_param

  bind_param_array

  bind_param_inout

  can

  clone

  column_info

  commit

  connect

  connect_cached

  data_sources

  disconnect

  do

  dump_results

  err

  errstr

  execute

  execute_array

  execute_for_fetch

  fetch

  fetchall_arrayref

  fetchall_hashref

  fetchrow_array

  fetchrow_arrayref

  fetchrow_hashref

  finish

  foreign_key_info

  func

  get_info

  installed_versions


  last_insert_id

  looks_like_number

  neat

  neat_list

  parse_dsn

  parse_trace_flag

  parse_trace_flags

  ping

  prepare

  prepare_cached

  primary_key

  primary_key_info

  quote

  quote_identifier

  rollback

  rows

  selectall_arrayref

  selectall_hashref

  selectcol_arrayref

  selectrow_array

  selectrow_arrayref

  selectrow_hashref

  set_err

  state

  table_info

  table_info_all

  tables

  trace

  trace_msg

  type_info

  type_info_all

  Attributes for Handles

###### PHP API - using functions built into PHP with MySQL

  mysql_affected_rows

  mysql_change_user

  mysql_client_encoding

  mysql_close

  mysql_connect

  mysql_create_db

  mysql_data_seek

  mysql_db_name

  mysql_db_query

  mysql_drop_db

  mysql_errno

  mysql_error

  mysql_escape_string

  mysql_fetch_array

  mysql_fetch_assoc

  mysql_fetch_field

  mysql_fetch_lengths

  mysql_fetch_object

  mysql_fetch_row

  mysql_field_flags

  mysql_field_len

  mysql_field_name

  mysql_field_seek

  mysql_field_table

  mysql_field_type

  mysql_free_result

  mysql_get_client_info

  mysql_get_host_info

  mysql_get_proto_info

  mysql_get_server_info

  mysql_info

  mysql_insert_id

  mysql_list_dbs

  mysql_list_fields

  mysql_list_processes

  mysql_list_tables

  mysql_num_fields

  mysql_num_rows

  mysql_pconnect

  mysql_ping

  mysql_query

  mysql_real_escape_string

  mysql_result

  mysql_select_db

  mysql_stat

  mysql_tablename

  mysql_thread_id

  mysql_unbuffered_query


#### Time / Timezones:
```
SELECT CONVERT_TZ(displaytime,'GMT','MET');
should work if your column type is timestamp, or date
You need to have the timezones loaded. See below if you don't have the timezones loaded.
```
```
