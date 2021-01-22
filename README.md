[![Build Status](https://circleci.com/gh/letsencrypt/mariadb-autoincrement-partition-manager-py.svg?style=shield)](https://circleci.com/gh/letsencrypt/mariadb-autoincrement-partition-manager-py)
![Maturity Level: Beta](https://img.shields.io/badge/maturity-beta-blue.svg)

This tool partitions and manages MariaDB tables by autoincrement IDs.

Note that partitioning is not a fast operation on ext4 filesystems; it is fast on xfs and zfs.

Similar tools:
* https://github.com/davidburger/gomypartition, intended for tables with date-based partitions
* https://github.com/yahoo/mysql_partition_manager, which is arcihved and in pure SQL

# Usage

```sh
 → autoincrement-partition-manager --db dbname --table tablename \
    --mariadb test_tools/fake_mariadb.sh --log-level=debug \
    add_partition --noop
DEBUG:root:Auto_Increment column identified as id
DEBUG:root:Partition range column identified as id
DEBUG:root:Found partition before = (100)
DEBUG:root:Found tail partition named p_20201204
INFO:root:No-op mode

ALTER TABLE `dbname`.`tablename` REORGANIZE PARTITION `p_20201204` INTO (PARTITION `p_20201204` VALUES LESS THAN (3101009), PARTITION `p_20210122` VALUES LESS THAN MAXVALUE);

```

# TODOs

Lots. A drop mechanism, for one. Yet more tests, particularly live integration tests with a test DB, for another.
