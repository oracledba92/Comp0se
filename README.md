I have taken the provided pitr and improved it in several ways ...

(1) Improved argument handling making the usage much clearer 

usage: pitr [-h] --source SourceDir --wal WalDir --destination DestDir
            [--recovery_option E|L|T|R|X]
            [--post_action pause|promote|shutdown]
            [--recovery_time "YYYY-mm-dd HH:MM:SS" | --recovery_point RestorePoint | --recovery_xid Xid]

Run a point in time restore for Postgres.

optional arguments:
  -h, --help            show this help message and exit
  --source SourceDir    source directory of the Postgres.
  --wal WalDir          wal archive directory.
  --destination DestDir
                        destination directory.
  --recovery_option E|L|T|R|X
                        recovery type [(E)arliest, (L)atest, (T)ime, (R)estore
                        point, (X)id]
  --post_action pause|promote|shutdown
                        post recovery action [pause|promote|shutdown(default)]
  --recovery_time "YYYY-mm-dd HH:MM:SS"
                        time to restore to (YYYY-mm-dd HH:MM:SS)
  --recovery_point RestorePoint
                        name of the restore point to be used.
  --recovery_xid Xid    xid to restore to.

(2) Output (both normal and debug) have been added. DEBUG can be set in the environment to receive more detailed information

(3) Additional functionality - the original script only accepted a timestamp - the improved version can cope with a restore point
or Xid or simply restore to the earliest or latest possible points given the supplied WALs.

(4) New Features. The script uses the 9.5 new functionality, but can also drop back to pre-9.5 functionality.
