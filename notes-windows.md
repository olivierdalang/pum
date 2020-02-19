# Notes for Windows (requires cleanup)

## Using

```
# create virtualenv
virtualenv C:\Users\YOUR_USERNAME\.virtualenvs\testing_pum

# activate virtualenv
C:\Users\YOUR_USERNAME\.virtualenvs\testing_pum\Scripts\activate.ps1

# install pum
pip install pum

# running
pum dump -p pg_qgep test.txt
>>> FileNotFoundError: [WinError 2] The system cannot find the file specified
```

**Issue : we need pg_dump.exe**

From [this](https://wiki.postgresql.org/wiki/Automated_Backup_on_Windows#Files_needed_to_run_pg_dump_.26_pg_dumpall), it seems pg_dump.exe is only distributed with postgres_server.

[Download the binaries](https://www.enterprisedb.com/download-postgresql-binaries), and copy all files from `pgsql\bin` to `C:\Users\YOUR_USERNAME\.virtualenvs\testing_pum\Scripts\`.

ALTERNATIVE

Create following  `my_config.yml`
```
pg_dump_exe: C:\Users\Olivier\Downloads\postgresql-12.2-1-windows-x64-binaries\pgsql\bin\pg_dump.exe
pg_restore_exe: C:\Users\Olivier\Downloads\postgresql-12.2-1-windows-x64-binaries\pgsql\bin\pg_restore.exe
```

Then
```
# running with config file
pum -c my_config.yml dump -p pg_qgep test.txt
```

## Testing

```
# create virtualenv
virtualenv C:\Users\YOUR_USERNAME\.virtualenvs\testing_pum

# activate virtualenv
C:\Users\YOUR_USERNAME\.virtualenvs\testing_pum\Scripts\activate.ps1

# install source
git clone https://github.com/opengisch/pum.git
pip install -e .\pum

cd pum

# run tests (requires a bash capable terminal e.g. gitbash)
.\.ci\setup_db.sh
nose2 -v
.\test\test_pum.sh

```

**Issue 2 : several tests fail fail**

Fixes incomming.
