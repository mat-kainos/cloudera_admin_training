# Start of lab - no tables, kerberos users and table grants
~~~
kinit mat-kainos/admin@GDANSKBDA.COM
Password for mat-kainos/admin@GDANSKBDA.COM:
klist
Ticket cache: FILE:/tmp/krb5cc_1001
Default principal: mat-kainos/admin@GDANSKBDA.COM

Valid starting       Expires              Service principal
05/23/2019 12:58:42  05/24/2019 12:58:42  krbtgt/GDANSKBDA.COM@GDANSKBDA.COM
	renew until 05/30/2019 12:58:42

[mat-kainos@ip-172-31-31-233 ~]$ beeline
Beeline version 1.1.0-cdh5.14.4 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-31-233.eu-west-1.compute.internal@GDANSKBDA.COM
scan complete in 2ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-31-233.eu-west-1.compute.internal@GDANSKBDA.COM
Connected to: Apache Hive (version 1.1.0-cdh5.14.4)
Driver: Hive JDBC (version 1.1.0-cdh5.14.4)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20190523130505_68ba5462-eda5-4805-a041-44bf2efe9164): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190523130505_68ba5462-eda5-4805-a041-44bf2efe9164); Time taken: 0.537 seconds
INFO  : Executing command(queryId=hive_20190523130505_68ba5462-eda5-4805-a041-44bf2efe9164): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523130505_68ba5462-eda5-4805-a041-44bf2efe9164); Time taken: 0.298 seconds
INFO  : OK
+-----------+--+
| tab_name  |
+-----------+--+
+-----------+--+
No rows selected (2.123 seconds)
0: jdbc:hive2://localhost:10000/default>

~~~
# Creation of roles, grants and groups

~~~ 

Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-31-233.eu-west-1.compute.internal@GDANSKBDA.COM
Connected to: Apache Hive (version 1.1.0-cdh5.14.4)
Driver: Hive JDBC (version 1.1.0-cdh5.14.4)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> CREATE ROLE reads;
INFO  : Compiling command(queryId=hive_20190523133131_da79a3ce-8a39-4072-bb55-cd1eaaad7e9f): CREATE ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133131_da79a3ce-8a39-4072-bb55-cd1eaaad7e9f); Time taken: 0.062 seconds
INFO  : Executing command(queryId=hive_20190523133131_da79a3ce-8a39-4072-bb55-cd1eaaad7e9f): CREATE ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133131_da79a3ce-8a39-4072-bb55-cd1eaaad7e9f); Time taken: 0.022 seconds
INFO  : OK
No rows affected (0.126 seconds)
0: jdbc:hive2://localhost:10000/default> show grant role reads;
INFO  : Compiling command(queryId=hive_20190523133131_cef380a2-a5cd-4eb7-acc5-1e98f46c612d): show grant role reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:database, type:string, comment:from deserializer), FieldSchema(name:table, type:string, comment:from deserializer), FieldSchema(name:partition, type:string, comment:from deserializer), FieldSchema(name:column, type:string, comment:from deserializer), FieldSchema(name:principal_name, type:string, comment:from deserializer), FieldSchema(name:principal_type, type:string, comment:from deserializer), FieldSchema(name:privilege, type:string, comment:from deserializer), FieldSchema(name:grant_option, type:boolean, comment:from deserializer), FieldSchema(name:grant_time, type:bigint, comment:from deserializer), FieldSchema(name:grantor, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133131_cef380a2-a5cd-4eb7-acc5-1e98f46c612d); Time taken: 0.074 seconds
INFO  : Executing command(queryId=hive_20190523133131_cef380a2-a5cd-4eb7-acc5-1e98f46c612d): show grant role reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133131_cef380a2-a5cd-4eb7-acc5-1e98f46c612d); Time taken: 0.042 seconds
INFO  : OK
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------+----------+--+
| database  | table  | partition  | column  | principal_name  | principal_type  | privilege  | grant_option  | grant_time  | grantor  |
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------+----------+--+
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------+----------+--+
No rows selected (0.168 seconds)
0: jdbc:hive2://localhost:10000/default> CREATE ROLE writes;
INFO  : Compiling command(queryId=hive_20190523133131_cd95e49d-bff5-4b44-82c4-29a70f115667): CREATE ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133131_cd95e49d-bff5-4b44-82c4-29a70f115667); Time taken: 0.053 seconds
INFO  : Executing command(queryId=hive_20190523133131_cd95e49d-bff5-4b44-82c4-29a70f115667): CREATE ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133131_cd95e49d-bff5-4b44-82c4-29a70f115667); Time taken: 0.008 seconds
INFO  : OK
No rows affected (0.071 seconds)
0: jdbc:hive2://localhost:10000/default> show grant role writes;
INFO  : Compiling command(queryId=hive_20190523133131_649db715-2e6e-4a14-8f61-37842f5ac2f9): show grant role writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:database, type:string, comment:from deserializer), FieldSchema(name:table, type:string, comment:from deserializer), FieldSchema(name:partition, type:string, comment:from deserializer), FieldSchema(name:column, type:string, comment:from deserializer), FieldSchema(name:principal_name, type:string, comment:from deserializer), FieldSchema(name:principal_type, type:string, comment:from deserializer), FieldSchema(name:privilege, type:string, comment:from deserializer), FieldSchema(name:grant_option, type:boolean, comment:from deserializer), FieldSchema(name:grant_time, type:bigint, comment:from deserializer), FieldSchema(name:grantor, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133131_649db715-2e6e-4a14-8f61-37842f5ac2f9); Time taken: 0.056 seconds
INFO  : Executing command(queryId=hive_20190523133131_649db715-2e6e-4a14-8f61-37842f5ac2f9): show grant role writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133131_649db715-2e6e-4a14-8f61-37842f5ac2f9); Time taken: 0.008 seconds
INFO  : OK
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------+----------+--+
| database  | table  | partition  | column  | principal_name  | principal_type  | privilege  | grant_option  | grant_time  | grantor  |
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------+----------+--+
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------+----------+--+
No rows selected (0.078 seconds)
0: jdbc:hive2://localhost:10000/default>





0: jdbc:hive2://localhost:10000/default> GRANT SELECT ON DATABASE default TO ROLE reads;
INFO  : Compiling command(queryId=hive_20190523133232_5e8c79f0-9cd0-4312-930d-e62410fd4593): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133232_5e8c79f0-9cd0-4312-930d-e62410fd4593); Time taken: 0.06 seconds
INFO  : Executing command(queryId=hive_20190523133232_5e8c79f0-9cd0-4312-930d-e62410fd4593): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133232_5e8c79f0-9cd0-4312-930d-e62410fd4593); Time taken: 0.011 seconds
INFO  : OK
No rows affected (0.081 seconds)
0: jdbc:hive2://localhost:10000/default> GRANT ROLE reads TO GROUP selector;
INFO  : Compiling command(queryId=hive_20190523133232_bd3d4c4a-8893-4247-a89d-436c4a6e43e6): GRANT ROLE reads TO GROUP selector
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133232_bd3d4c4a-8893-4247-a89d-436c4a6e43e6); Time taken: 0.052 seconds
INFO  : Executing command(queryId=hive_20190523133232_bd3d4c4a-8893-4247-a89d-436c4a6e43e6): GRANT ROLE reads TO GROUP selector
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133232_bd3d4c4a-8893-4247-a89d-436c4a6e43e6); Time taken: 0.009 seconds
INFO  : OK
No rows affected (0.071 seconds)
0: jdbc:hive2://localhost:10000/default> show grant role reads;
INFO  : Compiling command(queryId=hive_20190523133232_71be1f2b-5455-401a-a229-dc065dd4f746): show grant role reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:database, type:string, comment:from deserializer), FieldSchema(name:table, type:string, comment:from deserializer), FieldSchema(name:partition, type:string, comment:from deserializer), FieldSchema(name:column, type:string, comment:from deserializer), FieldSchema(name:principal_name, type:string, comment:from deserializer), FieldSchema(name:principal_type, type:string, comment:from deserializer), FieldSchema(name:privilege, type:string, comment:from deserializer), FieldSchema(name:grant_option, type:boolean, comment:from deserializer), FieldSchema(name:grant_time, type:bigint, comment:from deserializer), FieldSchema(name:grantor, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133232_71be1f2b-5455-401a-a229-dc065dd4f746); Time taken: 0.055 seconds
INFO  : Executing command(queryId=hive_20190523133232_71be1f2b-5455-401a-a229-dc065dd4f746): show grant role reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133232_71be1f2b-5455-401a-a229-dc065dd4f746); Time taken: 0.008 seconds
INFO  : OK
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------------+----------+--+
| database  | table  | partition  | column  | principal_name  | principal_type  | privilege  | grant_option  |    grant_time     | grantor  |
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------------+----------+--+
| default   |        |            |         | reads           | ROLE            | select     | false         | 1558618351025000  | --       |
+-----------+--------+------------+---------+-----------------+-----------------+------------+---------------+-------------------+----------+--+
1 row selected (0.084 seconds)
0: jdbc:hive2://localhost:10000/default>



0: jdbc:hive2://localhost:10000/default> show grant role writes;
INFO  : Compiling command(queryId=hive_20190523133535_7b57756d-bee6-428a-87e9-6d2cd7ec18ec): show grant role writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:database, type:string, comment:from deserializer), FieldSchema(name:table, type:string, comment:from deserializer), FieldSchema(name:partition, type:string, comment:from deserializer), FieldSchema(name:column, type:string, comment:from deserializer), FieldSchema(name:principal_name, type:string, comment:from deserializer), FieldSchema(name:principal_type, type:string, comment:from deserializer), FieldSchema(name:privilege, type:string, comment:from deserializer), FieldSchema(name:grant_option, type:boolean, comment:from deserializer), FieldSchema(name:grant_time, type:bigint, comment:from deserializer), FieldSchema(name:grantor, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133535_7b57756d-bee6-428a-87e9-6d2cd7ec18ec); Time taken: 0.055 seconds
INFO  : Executing command(queryId=hive_20190523133535_7b57756d-bee6-428a-87e9-6d2cd7ec18ec): show grant role writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133535_7b57756d-bee6-428a-87e9-6d2cd7ec18ec); Time taken: 0.008 seconds
INFO  : OK
+-----------+------------+------------+---------+-----------------+-----------------+------------+---------------+-------------------+----------+--+
| database  |   table    | partition  | column  | principal_name  | principal_type  | privilege  | grant_option  |    grant_time     | grantor  |
+-----------+------------+------------+---------+-----------------+-----------------+------------+---------------+-------------------+----------+--+
| default   | sample_07  |            |         | writes          | ROLE            | select     | false         | 1558618453695000  | --       |
+-----------+------------+------------+---------+-----------------+-----------------+------------+---------------+-------------------+----------+--+
1 row selected (0.14 seconds)
0: jdbc:hive2://localhost:10000/default> show role grant group inserters;
INFO  : Compiling command(queryId=hive_20190523133636_b43ce253-b713-4f70-a9a1-603b46ec54b4): show role grant group inserters
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:role, type:string, comment:from deserializer), FieldSchema(name:grant_option, type:boolean, comment:from deserializer), FieldSchema(name:grant_time, type:bigint, comment:from deserializer), FieldSchema(name:grantor, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133636_b43ce253-b713-4f70-a9a1-603b46ec54b4); Time taken: 0.062 seconds
INFO  : Executing command(queryId=hive_20190523133636_b43ce253-b713-4f70-a9a1-603b46ec54b4): show role grant group inserters
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133636_b43ce253-b713-4f70-a9a1-603b46ec54b4); Time taken: 0.013 seconds
INFO  : OK
+---------+---------------+-------------+----------+--+
|  role   | grant_option  | grant_time  | grantor  |
+---------+---------------+-------------+----------+--+
| writes  | false         | NULL        | --       |
+---------+---------------+-------------+----------+--+
1 row selected (0.09 seconds)
0: jdbc:hive2://localhost:10000/default>

~~~


# Testing grants for users george and ferdinand 
##### ferdinand can access table sample_07 while george can access sample_07 and employee
#
~~~
[mat-kainos@ip-172-31-31-233 ~]$ kinit george
Password for george@GDANSKBDA.COM:
[mat-kainos@ip-172-31-31-233 ~]$ klist
Ticket cache: FILE:/tmp/krb5cc_1001
Default principal: george@GDANSKBDA.COM

Valid starting       Expires              Service principal
05/23/2019 13:36:50  05/24/2019 13:36:50  krbtgt/GDANSKBDA.COM@GDANSKBDA.COM
	renew until 05/30/2019 13:36:50
[mat-kainos@ip-172-31-31-233 ~]$ beeline
Beeline version 1.1.0-cdh5.14.4 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-31-233.eu-west-1.compute.internal@GDANSKBDA.COM
scan complete in 2ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-31-233.eu-west-1.compute.internal@GDANSKBDA.COM
Connected to: Apache Hive (version 1.1.0-cdh5.14.4)
Driver: Hive JDBC (version 1.1.0-cdh5.14.4)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> show tables;
INFO  : Compiling command(queryId=hive_20190523133737_c64732c6-6fac-4fbe-bd63-10d128bde9e5): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133737_c64732c6-6fac-4fbe-bd63-10d128bde9e5); Time taken: 0.063 seconds
INFO  : Executing command(queryId=hive_20190523133737_c64732c6-6fac-4fbe-bd63-10d128bde9e5): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133737_c64732c6-6fac-4fbe-bd63-10d128bde9e5); Time taken: 0.103 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| employee   |
| sample_07  |
+------------+--+
2 rows selected (0.238 seconds)
0: jdbc:hive2://localhost:10000/default> !quit
Closing: 0: jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-31-233.eu-west-1.compute.internal@GDANSKBDA.COM
[mat-kainos@ip-172-31-31-233 ~]$ kdestroy
[mat-kainos@ip-172-31-31-233 ~]$ klist
klist: No credentials cache found (filename: /tmp/krb5cc_1001)
[mat-kainos@ip-172-31-31-233 ~]$ kinit ferdinand
Password for ferdinand@GDANSKBDA.COM:
[mat-kainos@ip-172-31-31-233 ~]$ klist
Ticket cache: FILE:/tmp/krb5cc_1001
Default principal: ferdinand@GDANSKBDA.COM

Valid starting       Expires              Service principal
05/23/2019 13:38:05  05/24/2019 13:38:05  krbtgt/GDANSKBDA.COM@GDANSKBDA.COM
	renew until 05/30/2019 13:38:05
[mat-kainos@ip-172-31-31-233 ~]$ beeline
Beeline version 1.1.0-cdh5.14.4 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-31-233.eu-west-1.compute.internal@GDANSKBDA.COM
scan complete in 1ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-31-233.eu-west-1.compute.internal@GDANSKBDA.COM
Connected to: Apache Hive (version 1.1.0-cdh5.14.4)
Driver: Hive JDBC (version 1.1.0-cdh5.14.4)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> show tables;
INFO  : Compiling command(queryId=hive_20190523133838_445a284d-dd10-46ae-8dc6-51e8b3ff1693): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20190523133838_445a284d-dd10-46ae-8dc6-51e8b3ff1693); Time taken: 0.06 seconds
INFO  : Executing command(queryId=hive_20190523133838_445a284d-dd10-46ae-8dc6-51e8b3ff1693): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20190523133838_445a284d-dd10-46ae-8dc6-51e8b3ff1693); Time taken: 0.094 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| sample_07  |
+------------+--+
1 row selected (0.226 seconds)
0: jdbc:hive2://localhost:10000/default>
~~~