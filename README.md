# Paperang(喵喵机) Python API

### Requirements & Dependencies

<<<<<<< Updated upstream
OS: Linux

Python: 3.5-3.7 (tested)

`pybluez` Needed by operating on the system bluetooth stack
 
`cv2, numpy` 图像转换工具需要

### 建立连接
=======
OS: OSX (tested on Catalina)/Linux (tested Debian Buster on a Raspberry Pi 4)  
Python: 3.5-3.7 (tested)

Required debian packages: `libbluetooth-dev libhidapi-dev libatlas-base-dev python3-llvmlite python3-numba python-llvmlite llvm-dev`

Python Modules: install with `pip3 install -r requirements.txt`

### macOS instructions

#### Set up and test your printer

You'll need python3 installed; check if you have it by typing `which python3` in Terminal or your favorite console application.

1. Install necessary python modules:

```sh
pip3 install -r requirements.txt
```

Note: you may need to install pybluez manually if this fails via `pip uninstall pybluez pip install git+https://github.com/pybluez/pybluez.git`

2. Ensure bluetooth is enabled on your computer. You do _not_ need to connect your Paperang to your computer yet! We'll do that later, via the command line.
3. Turn on your Paperang and set it near your computer
4. Run the test script, which will tell your Paperang to print a self-test if it's successful:

```sh
python3 testprint.py
```

If you've never paired your Paperang with your computer, you might get a dialog asking you to allow the Paperang to pair with your system. Click `connect`. You should only have to do this once.

5. If the test print was successful, the script will print out your device's MAC address on the console, as well as on the printer. You can enter that into the script to connect to your Paperang directly, avoiding the wait time for scanning for printers.

If you need to look up your Paperang's MAC address quickly, you can use the `system_profiler` command to output information on all paired bluetooth devices:

```sh
system_profiler SPBluetoothDataType
```

#### Print Little Printer data

### Establishing a connection
>>>>>>> Stashed changes

`BtManager()` 参数留空会搜索附近可用的喵喵机并连接

`BtManager("AA:BB:CC:DD:EE:FF")` 附加指定MAC会跳过搜索过程直接连接设备，更省时间

### 打印图像

从API看该机器只能输入二值图像进行打印，所以文本转图片是在客户端完成的。

打印的图像格式为二进制数据，每一位表示黑(1)或白(0)，每行384个点。

```python
mmj = BtManager()
mmj.sendImageToBt(img)
mmj.disconnect()
```

### 其他杂项

`registerCrcKeyToBt(key=123456)` 更改通信 CRC32 KEY(不太懂这么做是为了啥,讲道理监听到这个包就能拿到 key 的)

`sendPaperTypeToBt(paperType=0)` 更改纸张类型(疯狂卖纸呢)

`sendPowerOffTimeToBt(poweroff_time=0)` 更改自动关机时间

`sendSelfTestToBt()` 打印自检页面

`sendDensityToBt(density)` 设置打印密度

`sendFeedLineToBt(length)` 控制打印完后的 padding

`queryBatteryStatus()` 查询剩余电量

`queryDensity()` 查询打印密度

`sendFeedToHeadLineToBt(length)` 不太懂和 `sendFeedLineToBt` 有什么区别，但是看起来都是在打印后调用的。

`queryPowerOffTime()` 查询自动关机时间

`querySNFromBt()` 查询设备 SN

其实还有挺多操作的，有兴趣的看着`const.py`猜一猜好了。

### 图像工具

`ImageConverter.image2bmp(path)` 任意图像到可供打印的二进制数据转换

`TextConverter.text2bmp(text)` 指定文字到可供打印的二进制数据转换

### 微信公众平台工具

两个小脚本，用来实现发送图片给微信公众号后自动打印。

`wechat.php` 用于 VPS 接收腾讯数据，默认只允许指定用户打印。

`printer_server.py` 放置于树莓派等有蓝牙的靠近喵喵机的机器上运行，可以使用`tinc`等建立 VPN 以供 VPS 直接访问。

### 吐槽

这玩意就不能增加一个多次打印的功能吗？以较低温度多次打印再走纸，应该可以实现打印灰度图的。

逆了好久的固件也没搞出来啥东西，真是菜。希望有大佬能告诉我一点人生的经验。

顺便丢两个芯片型号: `NUC123LD4BN0`, `STM32F071CBU6`，似乎是 Cortex-M0。

PS: 本代码仅供非盈利用途，如用于商业用途请另请高明。

### Acknowledgement 致谢

<<<<<<< Updated upstream

=======
Thanks for all the reverse engineering work done by the original author of this project.
>>>>>>> Stashed changes
