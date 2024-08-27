# Backup and Restore PostgreSQL

## 1. Backup

### 1.1 Backup the entire database
```
docker exec -t indexer_db pg_dump -U postgres -d postgres -F c -f /var/lib/postgresql/data/postgres.dump
```
- -U postgres: PostgreSQL username.
- -d postgres: Database name (postgres).
- -F c: Backup format (custom format).
- -f /var/lib/postgresql/data/postgres.dump: Path and filename of the backup file within the container.

### 1.2 Backup a specific schema
#### 1.2.1 Backup a specific schema with Custom Format (-F c):
```
docker exec -t indexer_db pg_dump -U postgres -d postgres --schema=schema_qmrwisx41srrr8f -F c -f /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump
```
- --schema=schema_qmrwisx41srrr8f: Specifies the schema you want to back up.
- -F c: Backup format (custom format).
- -f /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump: Path and filename of the backup file within the container.

#### 1.2.2 Backup a specific schema with Directory Format (-F d):
```
docker exec -t indexer_db pg_dump -U postgres -d postgres -F d -f /var/lib/postgresql/data/postgres_directory
```
- --schema=schema_qmrwisx41srrr8f: Specify the schema you want to backup.
- -F d: Backup format (Directory format). This method will restore faster when using restore with multiple parallel jobs.
- -f /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump: Path and name of the backup file in the container.

## 2. Restore

### Restore from backup file
1. Copy the backup file to the directory /root/subquery-indexer/.data/postgres/:
    ```
    cp /root/schema_qmrwisx41srrr8f.dump /root/subquery-indexer/.data/postgres/schema_qmrwisx41srrr8f.dump
    ```

2. Create a new tmux session:
    ```
    tmux new -s restore_qmrwisx41srrr8f
    ```

3. Restore data from the backup file:
    ```
    docker exec -it indexer_db pg_restore -v -j 5 -U postgres -d postgres /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump > /root/restore_qmrwisx41srrr8f.log 2>&1
    ```
    - -v: Verbose mode.
    - -j 5: Use 5 parallel jobs.
    - -U postgres: PostgreSQL username.
    - -d postgres: Target database name (postgres).
    - /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump: Path to the backup file in the container.
    - /root/restore_qmrwisx41srrr8f.log 2>&1: Write all output and errors to the log file restore_qmrwisx41srrr8f.log.

## Other commands

### Drop schema
## 2. Restore

### Restore from a backup file
1. Copy the backup file to the /root/subquery-indexer/.data/postgres/ directory:
    ```
    cp /root/schema_qmrwisx41srrr8f.dump /root/subquery-indexer/.data/postgres/schema_qmrwisx41srrr8f.dump
    ```

2. Create a new tmux session:
    ```
    tmux new -s restore_qmrwisx41srrr8f
    ```

3. Restore the data from the backup file:
    ```
    docker exec -it indexer_db pg_restore -v -j 5 -U postgres -d postgres /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump > /root/restore_qmrwisx41srrr8f.log 2>&1
    ```
    - -v: Verbose mode.
    - -j 5: Use 5 parallel jobs.
    - -U postgres: PostgreSQL username.
    - -d postgres: Target database name (postgres).
    - /var/lib/postgresql/data/schema_qmrwisx41srrr8f.dump: Path to the backup file within the container.
    - /root/restore_qmrwisx41srrr8f.log 2>&1: Redirects all output and errors to the restore_qmrwisx41srrr8f.log file.

## Other Commands

### Drop schema
```
docker exec -it indexer_db psql -U postgres -d postgres -c "DROP SCHEMA IF EXISTS schema_qmvkg3gjejcpwkx CASCADE;"
```
### Log restore output
To view the restore log, use the following command:
```
cat /root/restore_qmrwisx41srrr8f.log
```