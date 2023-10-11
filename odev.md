## Databases list
The file at `~/.config/odev/databases.cfg` contains the list of Odoo databases and attributes. The command `odev list` reads data from here.
> Sometimes it might be necessary to manually remove a database from this file. 

### Example file
```
[15.0-test]
last_run = 2023-10-11T11:48:19.436598
version_clean = 15.0
enterprise = enterprise

[16.0-test]
last_run = 2023-09-11T11:48:19.436598
version_clean = 16.0
enterprise = enterprise
```

```bash
vi ~/.config/odev/databases.cfg
``` 
