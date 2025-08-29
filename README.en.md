# segger-defmt
## open JlinkGDBServer, select your chip and click OK
## create `./run.sh` in your project
```
cp $1 $1.elf # JLinkExe need file suffix

ELF_FILE="$1.elf"

JLinkExe <<EOF
Device nrf52840_xxaa
SelectInterface SWD
Speed 4000
LoadFile ${ELF_FILE}
r
g
q
EOF

defmt-print -e $1 tcp
```
## edit `.cargo/config.toml`
```
runner = "./run.sh"
```