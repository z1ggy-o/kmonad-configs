# 使用方法

- config 语法
	- 注释：`#|`，`|#` 是 block, `;;` 是 line
	- 其余内容都是 Lisp like 的括号方式

- config 内容
	- `defcfg`: 必有的 block, 至少需要有 `input` 和 `output` 两个配置来知道从哪里获取输入，发送输出
		- input 可以从 `/dev/input/by-path` 和 `/dev/input/by-id` 中获得。推荐使用 by-id, 因为插拔之后也不会变。
		- output 依赖于 `uinput` 设备，所以需要保证 `uinput` module 被载入了

- 使用 systemd 调用不同的 config
	- 利用 repo 里的 systemd script 作为模板，修改 kmonad 和 config 文件的路径
	- script 放到 `/etc/systemd/system/` 下面，然后调用 `systemctl daemon-reload` 之后，就可以启用添加的 script 了
	- 如果不修改 config 地址，则需要把 config 放到 `/etc/kmonad/` 下面
	- 利用 `sudo systemctl start kmonad@name` 来调用不同的 config
