# WIP for porting Icecream to FreeBSD
Do not drop it directly in /usr/ports because this will overwrite GIDs and UIDs.

## TODO
- ~~Fix the rc scripts so they work as they should~~
- ~~Get it to build with LLVM and remove GCC as dependency~~
- ~~Make a README~~
- Test that it actually works
- Make portlint happy

## RC VARIABLES (with example values)
### iceccd
- iceccd_enable="yes"
- iceccd_networkname="testnet"
- iceccd_basedir="/var/cache/ice"
- iceccd_logfile="/var/log/ice.log"
- iceccd_maxprocs="2"
- iceccd_nodename="mynode"
- iceccd_cachelimit="50"
- iceccd_scheduler="hostname:1234"

### icecc-scheduler
- icecc_scheduler_enable="YES"
- icecc_scheduler_netname="testnet"
- icecc_scheduler_port="1030"
- icecc_scheduler_logfile="/var/log/icecc-scheduler.log"
- icecc_scheduler_persistent="YES"
