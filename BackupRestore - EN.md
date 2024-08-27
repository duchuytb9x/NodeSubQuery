# Backup and Restore Database PostgreSQL

## 1. Backup

### 1.1 Backing Up the Entire Database

```
docker exec -t indexer_db pg_dump -U postgres -d postgres -F c -f /var/lib/postgresql/data/postgres.dump

```
- -U postgres: PostgreSQL username.

- -d postgres: Database name (postgres).

- -F c: Backup format (custom format).

- -f /var/lib/postgresql/data/postgres.dump: Backup file path and name in the container.

### 1.2 Backing up a specific schema
#### 1.2.1 Backing up a specific schema with Custom Format (-F c):
```
docker exec -t indexer_db pg_dump -U postgres -d postgres --schema=schema_qmrwisx41srrr8f -F c -f /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump
```
- --schema=schema_qmrwisx41srrr8f: Specify the schema you want to back up.

- -F c: Backup format (custom format).

- -f /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump: Backup file path and name in the container.

#### 1.2.2 Back up a specific schema with Directory Format (-F d):
```
docker exec -t indexer_db pg_dump -U postgres -d postgres -F d -f /var/lib/postgresql/data/postgres_directory -n schema_qmrwisx41srrr8f
```
- --schema=schema_qmrwisx41srrr8f: Specify the schema you want to back up.

- -F d: Backup format (Directory format). This will restore faster when using restore in combination with multiple parallel streams.

- -f /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump: Backup file path and name in the container.

## 2. Restore

### 2.1 Restore from backup
1. Copy the backup file to the /root/subquery-indexer/.data/postgres/ directory:
```
cp /root/schema_qmrwisx41srrr8f.dump /root/subquery-indexer/.data/postgres/schema_qmrwisx41srrr8f.dump
```

2. Create a new tmux session:
```
tmux new -s restore_qmrwisx41srrr8f
```

3. Restore data from backup:
```
docker exec -it indexer_db pg_restore -v -j 5 -U postgres -d postgres /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump > /root/restore_qmrwisx41srrr8f.log 2>&1
```
- -v: Verbose mode.

- -j 5: Use 5 parallel processes.

- -U postgres: PostgreSQL user name.

- -d postgres: Destination database name (postgres).

- /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump: Path to the backup file in the container.

- /root/restore_qmrwisx41srrr8f.log 2>&1: Write all output and errors to the restore_qmrwisx41srrr8f.log log file.

4. Restore data from backup directory:

```
#Create schema before restore
docker exec -it indexer_db psql -U postgres -d postgres -c "CREATE SCHEMA schema_qmvkg3gjejcpwkx;"
```

```
docker exec -it indexer_db pg_restore -v -j 5 -U postgres -d postgres -F d /var/lib/postgresql/data/postgres_directory --schema=restore_qmrwisx41srrr8f --no-owner > /root/restore_qmrwisx41srrr8f.log 2>&1
```
- -v: Verbose mode.

- -j 5: Use 5 parallel processes.

- -U postgres: PostgreSQL username.
- -d postgres: The name of the target database (postgres).

- /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump: The path to the backup file in the container.

- /root/restore_qmrwisx41srrr8f.log 2>&1: Write all output and errors to the restore_qmrwisx41srrr8f.log log file.

- --no-owner: Ignore ownership information of objects during restore, this is useful when you don't want to restore ownership or if the ownership from the backup is not compatible with the current user.

## Other commands

### Remove schema
```
docker exec -it indexer_db psql -U postgres -d postgres -c "DROP SCHEMA IF EXISTS schema_qmvkg3gjejcpwkx CASCADE;"
```
### Restore log output
To view the restore log, use the following command:
```
cat /root/restore_qmrwisx41srrr8f.log
```
