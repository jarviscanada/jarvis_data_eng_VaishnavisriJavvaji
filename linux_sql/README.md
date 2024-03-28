#!/bin/bash

psql_host=$1
psql_port=$2
db_name=$3
psql_user=$4
psql_password=$5

# Check # of args
if [ "$#" -ne 5 ]; then
echo "Illegal number of parameters"
exit 1
fi

# save hostname as a variable
hostname=$(hostname -f)

# save the number of CPUs to a variable
lscpu_out=`lscpu`
cpu_number=$(echo "$lscpu_out"  | egrep "^CPU\(s\):" | awk '{print $2}' | xargs)
# tip: `xargs` is a trick to remove leading and trailing white spaces
# tip: the $2 is instructing awk to find the second field

# hardware info
hostname=
cpu_number=
cpu_architecture=
cpu_model=
cpu_mhz=
l2_cache=
total_mem= $(vmstat --unit M | tail -1 | awk '{print $4}')
timestamp= # current timestamp in `2019-11-26 14:40:19` format; use `date` cmd

exit 0