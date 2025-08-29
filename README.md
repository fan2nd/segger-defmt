# segger-defmt
## 打开JLinkGDBServer,选好芯片,点击OK
## 写shell脚本`./run.sh`
```
cp $1 $1.elf

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
## 修改`.cargo/config.toml`
```
runner = "./run.sh"
```