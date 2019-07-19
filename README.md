```
yum install golang -y

cat >>/etc/profile<<EOF
export GOROOT=/usr/lib/golang
export GOPATH=\$HOME/go
export PATH=\$PATH:\$GOROOT/bin
EOF

source /etc/profile

#安装rdr redisdump解析工具

cd $HOME/go
go get github.com/xueqiu/rdr

cd src/github.com/xueqiu/rdr

#修改端口 8090为58080
vim main.go

Value: 58080,

go build .
```


RDR: redis data reveal
=================================================

RDR(redis data reveal) is a tool to parse redis rdbfile. Comparing to [redis-rdb-tools](https://github.com/sripathikrishnan/redis-rdb-tools), RDR is implemented by golang, much faster (5GB rdbfile takes about 2mins on my PC).

## Usage

```
NAME:
   rdr - a tool to parse redis rdbfile

USAGE:
   rdr [global options] command [command options] [arguments...]

VERSION:
   v0.0.1

COMMANDS:
     show     show statistical information of rdbfile by webpage
     keys     get all keys from rdbfile
     help, h  Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h     show help
   --version, -v  print the version
```

```
NAME:
   rdr show - show statistical information of rdbfile by webpage

USAGE:
   rdr show [command options] FILE1 [FILE2] [FILE3]...

OPTIONS:
   --port value, -p value  Port for rdr to listen (default: 8080)
```

```
NAME:
   rdr keys - get all keys from rdbfile

USAGE:
   rdr keys FILE1 [FILE2] [FILE3]...
```

[Linux amd64 Download](http://ohjx11q65.bkt.clouddn.com/rdr)

[OSX Download](http://ohjw7fr2u.bkt.clouddn.com/rdr)

[Windows Download](http://pb2xz7wd2.bkt.clouddn.com/rdr.exe)

After downloading maybe need add permisson to execute.

```
$ chmod a+x ./rdr
```

## Exapmle
```
$ ./rdr show -p 8080 *.rdb
```
Note that the memory usage is approximate.
![show example](http://ohjx11q65.bkt.clouddn.com/example.png)

```
$ ./rdr keys example.rdb
portfolio:stock_follower_count:ZH314136
portfolio:stock_follower_count:ZH654106
portfolio:stock_follower:ZH617824
portfolio:stock_follower_count:ZH001019
portfolio:stock_follower_count:ZH346349
portfolio:stock_follower_count:ZH951803
portfolio:stock_follower:ZH924804
portfolio:stock_follower_count:INS104806
```

## License

This project is under Apache v2 License. See the [LICENSE](LICENSE) file for the full license text.
