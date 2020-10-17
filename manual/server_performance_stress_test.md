# 服务器性能压力测试（Server performance stress test）

### 相关术语

- 响应时间(RT) ：指系统对请求作出响应的时间.
- 吞吐量(Throughput) ：指系统在单位时间内处理请求的数量
- QPS每秒查询率(Query Per Second) ：“每秒查询率”，是一台服务器每秒能够响应的查询次数，是对一个特定的查询服务器在规定时间内所处理流量多少的衡量标准。
- TPS(TransactionPerSecond)：每秒钟系统能够处理的交易或事务的数量
- 并发连接数：某个时刻服务器所接受的请求总数

### 测试工具（ab）

ab全称Apache Bench，是Apache自带的性能测试工具。使用这个工具，只须指定同时连接数、请求数以及URL，即可测试网站或网站程序的性能。

通过ab发送请求模拟多个访问者同时对某一URL地址进行访问,可以得到每秒传送字节数、每秒处理请求数、每请求处理时间等统计数据。

#### 安装程序

```bash
# 安装程序
$ sudo apt-get install apache2-utils
```

#### 命令格式

```bash
ab [options] [http://]hostname[:port]/path
```

#### 常用参数

```bash
-n requests 总请求数
-c concurrency 一次产生的请求数，可以理解为并发数
-t timelimit 测试所进行的最大秒数, 可以当做请求的超时时间
-p postfile 包含了需要POST的数据的文件
-T content-type POST数据所使用的Content-type头信息
```

#### 使用示例

```bash
# 测试GET请求
ab -n 10000 -c 100 -t 10 "http://10.22.102.201:8081/account/login"
# 测试POST请求
ab -n 10000 -c 100 -t 10 -p /home/dabolau/post.json "http://10.22.102.201:8081/account/login"
```

#### 请求参数（/home/dabolau/post.json）

```bash
{
    "usernmae": "username",
    "password": "password"
}
```

#### 输出结果

```bash
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 10.22.102.201 (be patient)
Finished 2104 requests


Server Software:        nginx/1.18.0
Server Hostname:        10.22.102.201
Server Port:            8081

Document Path:          /account/login
Document Length:        3373 bytes

Concurrency Level:      100
Time taken for tests:   10.001 seconds
Complete requests:      2104
Failed requests:        0
Total transferred:      7406872 bytes
HTML transferred:       7099396 bytes
Requests per second:    210.38 [#/sec] (mean)
Time per request:       475.341 [ms] (mean)
Time per request:       4.753 [ms] (mean, across all concurrent requests)
Transfer rate:          723.24 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        1   85 342.2     16    3271
Processing:     8  200 723.1     54    7388
Waiting:        6  141 409.1     53    6905
Total:         10  285 943.6     75    9566

Percentage of the requests served within a certain time (ms)
  50%     75
  66%     93
  75%    112
  80%    127
  90%    257
  95%   1637
  98%   2921
  99%   4781
 100%   9566 (longest request)

```

### 测试工具（wrk）

wrk是一款开源的HTTP性能测试工具，它和上面提到的ab同属于HTTP性能测试工具，它比ab功能更加强大，可以通过编写lua脚本来支持更加复杂的测试场景。

#### 安装程序

```bash
# 安装make工具
$ sudo apt install make
# 安装gcc编译环境
$ sudo apt install build-essential
# 安装git工具
$ sudo apt install git
# 克隆项目
$ git clone https://github.com/wg/wrk.git
# 进入项目根目录
$ cd wrk
# 使用make命令编译程序
$ make
```

编译成功后项目根目录中会出现wrk文件

#### 命令格式

```bash
wrk <options> <url>
```

#### 常用参数

```bash
-c --conections：保持的连接数
-d --duration：压测持续时间(s)
-t --threads：使用的线程总数
-s --script：加载lua脚本
-H --header：在请求头部添加一些参数
--latency 打印详细的延迟统计信息
--timeout 请求的最大超时时间(s)
```

#### 使用示例

```bash
./wrk -t 8 -c 100 --latency "http://10.22.102.201:8081/"
```

#### 输出结果

```bash
Running 10s test @ http://10.22.102.201:8081/
  8 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   224.39ms  179.85ms   1.83s    84.67%
    Req/Sec    38.21     23.25   111.00     67.67%
  Latency Distribution
     50%  205.25ms
     75%  275.95ms
     90%  339.32ms
     99%    1.22s 
  1965 requests in 10.01s, 8.35MB read
  Socket errors: connect 0, read 0, write 0, timeout 103
Requests/sec:    196.24
Transfer/sec:    854.17KB

```

### 测试工具（go-wrk）

go-wrk是Go语言版本的wrk，使用方法与wrk类似，Windows同学可以使用它来测试。

#### 安装程序

```bash
# 安装git工具
$ sudo apt install git
# 克隆项目
$ git clone https://github.com/adjust/go-wrk.git
# 进入项目根目录
$ cd go-wrk
# 开启go modules的情况，需要初始化配置(go1.11或以上)
$ go mod init go-wrk
# 使用命令编译程序
$ go build -o go-wrk
```

#### 命令格式

```bash
go-wrk [flags] url
```

#### 常用参数

```bash
-H="User-Agent: go-wrk 0.1 bechmark\nContent-Type: text/html;": 由'\n'分隔的请求头
-c=100: 使用的最大连接数
-k=true: 是否禁用keep-alives
-i=false: if TLS security checks are disabled
-m="GET": HTTP请求方法
-n=1000: 请求总数
-t=1: 使用的线程数
-b="" HTTP请求体
-s="" 如果指定，它将计算响应中包含搜索到的字符串s的频率
```

#### 使用示例

```bash
./go-wrk -t 8 -c 100 -n 10000 "http://10.22.102.201:8081/"
```

#### 输出结果

```bash
==========================BENCHMARK==========================
URL:				http://10.22.102.201:8081/

Used Connections:		100
Used Threads:			8
Total number of calls:		10000

===========================TIMINGS===========================
Total time passed:		26.16s
Avg time per request:		257.64ms
Requests per second:		382.24
Median time per request:	185.31ms
99th percentile time:		2190.88ms
Slowest time for request:	9751.00ms

=============================DATA=============================
Total response body sizes:		41800000
Avg response body per request:		4180.00 Byte
Transfer rate per second:		1597759.28 Byte/s (1.60 MByte/s)
==========================RESPONSES==========================
20X Responses:		10000	(100.00%)
30X Responses:		0	(0.00%)
40X Responses:		0	(0.00%)
50X Responses:		0	(0.00%)
Errors:			0	(0.00%)

```

