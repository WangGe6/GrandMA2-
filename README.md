# GrandMA2键盘

自定义手工打造的grandMA2编程区键盘,可发送MIDI信息控制控制台。

[<img src="https://user-images.githubusercontent.com/80170229/210251196-0c96b4aa-1008-4bc5-b2f8-234fe1ce431a.jpg" style="width: 25% "/>](https://user-images.githubusercontent.com/80170229/210251196-0c96b4aa-1008-4bc5-b2f8-234fe1ce431a.jpg)

* 键盘维护者: [Jonas Hartmann](https://github.com/hartmann-jonas)
* 使用的控制器: Raspberry Pi Pico
* 使用的开关: Cherry MX Black

## 部件:
电子部件
|数量	   |部件                                                     |购买地点 |
|---------|---------------------------------------------------------|-------------|
|70       |Cherry MX Black (与控制台感觉相同) |[德国](https://www.reichelt.de/de/en/cherry-mx-black-button-module-snap-on-attachment-cherry-mx1a-11nn-p202566.html?GROUPID=8099&START=0&OFFSET=16&SID=948d18f492480c7446a44c8ae52c183448e11f7a36750ce1244e6&LANGUAGE=EN&&r=1) (Germany)|
|70       |二极管 1N 914                                            |[德国](https://www.reichelt.de/de/en/rectifier-diode-do35-100-v-0-2-a-1n-914-p1763.html?nbc=1&&r=1) (Germany)|
|1        |Raspberry Pi Pico                                        |[德国](https://www.reichelt.de/de/en/raspberry-pi-pico-rp2040-cortex-m0-microusb-header-rasp-pi-pico-h-p305824.html?nbc=1&&r=1) (Germany)|
|1        |绝缘铜线                                    |[德国](https://www.reichelt.de/de/en/insulated-braided-copper-wire-10-m-1-x-0-14-mm-red-litze-rt-p10297.html?nbc=1&&r=1) (Germany)|

激光切割部件
|数量 |部件         |文件             |
|-------|-------------|-----------------|
|1      |顶板    |[top-plate.dxf](https://github.com/hartmann-jonas/GrandMA2-Keyboard/blob/main/dxf-files/top-plate.dxf)       |
|1      |开关板 |[switch-plate.dxf](https://github.com/hartmann-jonas/GrandMA2-Keyboard/blob/main/dxf-files/switch-plate.dxf) |
|1      |底板 |[bottom-plate.dxf](https://github.com/hartmann-jonas/GrandMA2-Keyboard/blob/main/dxf-files/bottom-plate.dxf) |
|1      |电缆板  |[cable-plate.dxf](https://github.com/hartmann-jonas/GrandMA2-Keyboard/blob/main/dxf-files/cable-plate.dxf)   |
|5      |侧板   |[wall-plate.dxf](https://github.com/hartmann-jonas/GrandMA2-Keyboard/blob/main/dxf-files/wall-plate.dxf)     |


## 指南:
*所有部件和板材都是必需的*

### 步骤1:
在开关板上放置所有开关

### 步骤2:
根据线路图焊接开关和二极管。不要立即将行和列焊接到pico上!

[<img src="https://raw.githubusercontent.com/hartmann-jonas/GrandMA2-Keyboard/main/images/soldering.jpeg" style="width: 80%"/>](https://raw.githubusercontent.com/hartmann-jonas/GrandMA2-Keyboard/main/images/soldering.jpeg)

焊接时不要将温度调太高。 对我来说 300°C 工作正常。

### 步骤3:
* 按照 这个 指南在微控制器上安装 KMK。 [this](https://github.com/KMKfw/kmk_firmware/blob/master/docs/en/Getting_Started.md) guide.
* 安装 KMK 后,需要用 这个文件 的内容替换你的 code.py 或 main.py 文件。 [this file](https://github.com/hartmann-jonas/GrandMA2-Keyboard/blob/main/code.py).

* 如果在尝试发送MIDI信息时遇到错误,您可能需要在微控制器上安装 [adafruit_midi](http://kmkfw.io/docs/midi/) adafruit_midi 库。

### 步骤4:
现在将行和列焊接到pico上
|行号    |Pico引脚 |列号     |Pico引脚 |
|-------|-----|-----------|-----|
|Row 0  |GP 5 |Column 0   |GP 4 |
|Row 1  |GP 8 |Column 1   |GP 3 |
|Row 2  |GP 6 |Column 2   |GP 2 |
|Row 3  |GP 7 |Column 3   |GP 1 |
|Row 4  |GP 9 |Column 4   |GP 0 |
|Row 5  |GP 10|Column 5   |GP 19|
|Row 6  |GP 11|Column 6   |GP 18|
|Row 7  |GP 12|Column 7   |GP 17|
|Row 8  |GP 13|Column 8   |GP 16|
|Row 9  |GP 14|
|Row 10 |GP 15|

### 步骤5:
* 在 GrandMA2 onPC 的 Midi In 设置中选择键盘
* 在 GrandMA2 onPC 中将midi音符映射到midi远程

### 线路图:
![keyboard](https://user-images.githubusercontent.com/80170229/210251995-ce025866-0632-42f6-a9ac-d74b289f22e6.svg)
[keyboard.pdf](https://github.com/hartmann-jonas/GrandMA2-Keyboard/files/10332369/keyboard.pdf)


### 固件:
固件使用 KMK 编写。 [KMK](http://kmkfw.io).


### Midi:
midi音符需要在每个不同的showfile中重新映射!

要将midi映射导入showfile,请将 [MA2_Keyboard.xml](https://github.com/hartmann-jonas/GrandMA2-Keyboard/blob/main/midi-mapping/MA2_Keyboard.xml) 复制到 GrandMA2 安装的 `importexport` 文件夹中,并运行导入命令
```
import "MA2_Keyboard" at remote 2
```
***注意***: 如果您的showfile中已经设置了midi映射,请确保midi音符号没有冲突。

## 在 GrandMA2 onPC 中设置
您需要将 GrandMA2 的远程输入设置中的“Note”值设置为以下表格:
|Midi Number|Key|
|--|-----------|
|0|Encoder Key |
|1|Tools       |
|2|Setup       |
|3|Backup      |
|4|Help        |
|5|Blind       |
|6|Freeze      |
|7|Preview     |
|8|Assign      |
|9|Align       |
|10|Fix        |
|11|Select     |
|12|Off        |
|13|View       |
|14|Effect     |
|15|Goto       |
|16|Del        |
|17|Temp       |
|18|Top        |
|19|On         |
|20|Page       |
|21|Macro      |
|22|Preset     |
|23|Copy       |
|24|<<<        |
|25|Learn      |
|26|>>>        |
|27|Sequ       |
|28|Cue        |
|29|Exec       |
|30|Go -       |
|31|Pause      |
|32|Go +       |
|33|Channel    |
|34|Fixture    |
|35|Group      |
|36|Move       |
|37|Time       |
|38|Esc        |
|39|7          |
|40|8          |
|41|9          |
|42|+          |
|43|Full       |
|44|Highlight  |
|45|Solo       |
|46|Edit       |
|47|Oops       |
|48|4          |
|49|5          |
|50|6          |
|51|Thru       |
|52|1          |
|53|2          |
|54|3          |
|55|-          |
|56|Up         |
|57|Update     |
|58|Clear      |
|59|0          |
|60|. (Dot)    |
|61|If         |
|62|At         |
|63|Previous   |
|64|Set        |
|65|Next       |
|66|Store      |
|67|MA         |
|68|Please     |
|69|Down       |
