# segger-defmt
## 打开JLinkGDBServer,选好芯片,点击OK
## 写jlink脚本`./download.jlink`
- `<your-chip>`替换成你自己的芯片名,可以去jflash中找
- `<your-elf>`不用管
- 其他部分根据情况调整
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
case "$(uname)" in
    Darwin*) sed -i "" 's|LoadFile.*|LoadFile '"$1"'.elf|' ./download.jlink;;
    Linux*) sed -i 's|LoadFile.*|LoadFile '"$1"'.elf|' ./download.jlink;;
esac
JLinkExe -CommandFile ./download.jlink
defmt-print -e $1.elf tcp
```
## 修改`.cargo/config.toml`
```
runner = "./run.sh"
```