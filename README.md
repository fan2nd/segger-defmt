# segger-defmt
## 打开JLinkGDBServer,选好芯片,点击OK
## 写jlink脚本`./download.jlink`
```
Device <your-chip>
SelectInterface SWD
Speed 4000
LoadFile <your-elf>
r
g
q
```
## 写shell脚本`./run.sh`
```
mv -f $1 $1.elf # jlinkexe需要根据后缀识别固件格式
# 此处可以根据$1替换jlink脚本中的<your-elf>
JLinkExe -CommandFile ./download.jlink
defmt-print -e $1.elf tcp
```
## 修改`.cargo/config.toml`
```
runner = "./run.sh"
```