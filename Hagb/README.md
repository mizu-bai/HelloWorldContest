# 用 unix shell 实现的 Hello world

## 运行

``` bash
sh 1.sh
```

## 思路

1. 原本考虑使用 `wget` 和 `curl` 进行请求，发现两者均含非法字符。其后考虑用 `nc` 向自己的服务器发起连接，接收服务器发送的数据。实际上是我用 frp 通过 <https://freefrp.net> 进行内网穿透（因为我没有短域名也没有 ipv4 公网地址，感谢服务提供者），理论上还可以用短域名和低位端口（如个位数端口）来减小长度。

    ```bash
    nc 107.173.89.246 23333
    ```

2. 用脚本自身的内容来制造一些输入重定向给 `nc`（即 `<$0`），迫使 `nc` 退出。这种方式只占3个字符，不比任何参数（包含多加的空格至少占 3 个字符）更长。如果可以允许脚本运行后不退出，这部分处理可以省去。

    ```bash
    nc 107.173.89.246 23333<$0
    ```
