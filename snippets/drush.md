# Utilities
```
# Send BDD to @stage
drush @stage sql-cli < db_name.sql

# Get BDD in local from @prod, the dump is done on the remote server you need to retrieve it via ftp for example
drush @prod sql-dump --result-file=../backup-YYYY.MM.DD.sql

# connect as user admin
drush uli admin
...


```

# Maintenances
## Vérify update (security only)
```
drush pm-updatestatus --security-only
```

# Ressources
- [drush 7 documentation](https://drushcommands.com/drush-7x/)