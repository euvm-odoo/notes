# Database Dumps
When working with clients, it is common to need a copy of their data (not just their modules) stored locally to remove risk of manipulating data. To achieve this, dumps are used

### Get dump from Odoo SaaS
To get a dump from an Odoo SaaS database, append the following to the end of the url: `/saas_worker/dump.sql.gz`.

### Get dump from Odoo SH
To get a dump from an Odoo SH database, access the support page at `/_odoo/support` and access the SH project page. From there, select the branch and create a backup to download.n

## 1. Create database
First, a database must be created 
```bash
createdb <db_name>
```

## 2. Dump sql file into new database
A dump file basically contains SQL queries to create and populate the tables. This should be fed to the psql interface of the database. 
```bash
psql <db_name> < <path_to_dump_sql>
```

## 3. Change credentials
By default, the dump contains the credentials used by the client. To be able to log in, these must be overwritten. Inside `psql <dbname>`, run
```sql
UPDATE ir_cron SET active='f';
UPDATE ir_mail_server SET active='f';
UPDATE res_users SET login='admin',password='admin',active='t' WHERE id=1;
UPDATE res_users SET login='admin2',password='admin',active='t' WHERE id=2;
UPDATE res_users SET login='admin',password=null,active='t',password_crypt='$pbkdf2-sha512$25000$WqsVQiiFkJIyxnjPmTPGGA$wFyWXkZTOzKD5ZXttnJUuaVJJeLiYRpk5Rf06N6QpH8c7KHGof9OSzjlv4EJLi3U.rxe.ag4QuEPSA7oW6F6Bg' WHERE id=1;
UPDATE res_users SET login='admin2',password=null,active='t',password_crypt='$pbkdf2-sha512$25000$WqsVQiiFkJIyxnjPmTPGGA$wFyWXkZTOzKD5ZXttnJUuaVJJeLiYRpk5Rf06N6QpH8c7KHGof9OSzjlv4EJLi3U.rxe.ag4QuEPSA7oW6F6Bg' WHERE id=2;
UPDATE ir_config_parameter SET value = '2040-01-01 00:00:00' WHERE key = 'database.expiration_date';
UPDATE ir_ui_view SET active = 'f' WHERE id in (SELECT id FROM ir_ui_view WHERE  name like '%saas trial assets%');
DELETE FROM ir_attachment WHERE name like '%assets';
```

----------------------------------------------------

[More info... (ES)](https://docs.google.com/document/d/1So74pW-V0xIbkaw5HYSodce5r5tq9MDf3dSBy9uE4WE/edit)
