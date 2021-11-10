<p align="center"><a href="https://www.100ask.net" target="_blank" rel="noopener noreferrer"><img width="100" src="http://wechatapppro-1252524126.file.myqcloud.com/appTVs2sJfo3933/image/b_u_5fb1e35c3d801_CUAzKqf9/knhb7p8x0j7u.png" alt="100ASK logo"></a></p>

<h2 align="center">100ASK Linux LVGL Desktop</h2>

100ASK Linux LVGL desktop 是一个 MIT 许可的开源项目。本项目主要目的是为大家提供一个嵌入式Linux GUI的参考解决方案：低内存占用、简洁美观的视觉效果、拓展性强的项目架构。

# 介绍(Introduction)

100ASK Linux LVGL desktop 是一个 MIT 许可的开源项目。该项目由 [百问网团队](https://www.100ask.net) 研发、发布，目的是为 100ASK_IMX6ULL、100ASK_STM32MP157开发板提供提供一个基础GUI，使用Makefile组织管理源码、基于GCC编译。通过修改少量的配置便在其他Linux、Linux开发板上运行。

项目效果演示视频：

## 快速开始
1. 配置开发环境
本项目的开发环境为： VMware Workstation + Ubuntu
如果是学习韦东山嵌入式Linux教程的小伙伴可以跳过这一步
需要搭建开发环境的请点击连接查看详细教程：xxxxxx
2. 配置交叉编译环境。如果工具链没有配置正确，可能会导致编译不通过，即使编译通过了也不能在目标平台上运行，请注意检查运行环境，编译环境。
3. 先克隆主仓库：git clone xxxxxxxx
4. 克隆主仓库后，同步子仓库模块： git submodule update --init --recursive
5. 后续更新子仓库模块： git submodule update --remote
6. 进入仓库根目录 `xxxxx` ，执行 `make clean && make` 开始编译
7. 提升编译速度。全速编译命令： `make clean && make -j$(nproc) RUN_JOBS=-j$(nproc)` 
"make -j$(nproc)" 的 **16** 是指定编译 **主桌面程序** 的内核线程数
"RUN_JOBS=j$(nproc)"的 **16** 是指定编译 **APP程序** 的内核线程数
Linux 下输入 `nproc` 命令返回的数字是你机器的线程数

## 仓库子模块说明

- [x] lv_100ask_demos：百问网 LVGL 示例仓库 (平台无关，可以在支持LVGL的任意平台编译运行)
- [x] lv_100ask_modules：百问网模块仓库 (此仓库为本项目而设，目的是为了提供一些通用的模块供本项目使用，并减少代码量和项目维护难度)
- [ ] lv_demos：LVGL 官方的示例(LVGL官方仓库)
- [x] lv_drivers：用于 LVGL 嵌入式 GUI 库的 TFT 和触摸板驱动程序(LVGL官方仓库)
- [x] lvgl：LVGL库，项目基于此仓库(LVGL官方仓库)

> 上面 √ 选上的是必选仓库，如果不需要可选仓库，请注意修改配置文件和 Makefile。

# 项目架构

## 目录说明
``` shell
├── assets  # 程序运行所需的资源，二次开发需要将里面的文件copy开发板的文件系统中
│   ├── icon # 桌面背景和APP图标。需要将icon文件夹copy到主桌面程序的同级目录下，或者可以修改代码，指定资源路径
│   └── services # DBus服务列表。增加APP后需要参考里面的格式新建服务文件，并将服务文件(不是整个文件夹)copy到dbus服务文件目录下：  /usr/share/dbus-1/servers
├── lv_100ask_app # APP程序(二次开发新的APP主要在这里添加自己的APP)
│   └── src
│       ├── general_app # 平台无关的通用APP
│       │   ├── general_2048_game # APP程序的目录
│       │   │   ├── obj # 编译过程输出文件存放在这里(执行后 make clean 会清除)，可执行文件放在项目根目录的 bin 目录下
│       │   │   └── src	# APP程序代码
│       │   ├── .......
│       └── imx6ull_app # 硬件相关的APP
│           ├── imx6ull_set_lan # APP程序的目录
│           ├── .......
├── lv_100ask_demos # 百问网平台无关的通用APP
│   ├── docs
│   └── src
│       ├── lv_100ask_demo_2048
│       ├── ......
├── lv_100ask_modules # 百问网模块仓库 (此仓库为本项目而设，目的是为了提供一些通用的模块供本项目使用，并减少代码量和项目维护难度)
│   ├── docs
│   └── src
│       ├── lv_100ask_boot_animation # 开机动画模块
│       ├── lv_100ask_dbus_handler # DBus消息处理模块
│       ├── lv_100ask_dbus_message_dispatch # 消息分发模块(目前是桌面主程序专用)
│       ├── lv_100ask_demo_assistive_touch # 辅助触摸悬浮球模块
│       └── lv_100ask_demo_init_icon # 桌面图标初始化模块(桌面主程序专用)
├── lv_demos # LVGL 官方的示例(LVGL官方仓库)
├── lv_drivers # 用于 LVGL 嵌入式 GUI 库的 TFT 和触摸板驱动程序(LVGL官方仓库)
├── lvgl # LVGL库，项目基于此仓库(LVGL官方仓库)
├── lv_lib_png # 显示png图片库(LVGL官方仓库)
├── bin	# 编译完成后，所有的可执行文件存放在这里(执行后 make clean 会清除)
└── obj # 桌面程序的编译过程输出文件存放在这里(执行后 make clean 会清除)，可执行文件放在项目根目录的 bin 目录下
```

# 程序说明
TODO
## 如何添加自己的程序


# 文档(Documentation)



# 技术支持(FAQs)

# Issues

# Changelog


# License
MIT


Copyright © 2019-2020 深圳百问网科技有限公司 All Rights Reserved.



# 关于作者

