#### apt search 和 apt-cache search 的区别
    
    apt search pylint
    apt-cache search pylint

#### 查看某个apt包信息

    apt show pylint

#### awk中如果分割符是[]要怎么处理

    awk –F ‘[][]’ // [is closed with ]， except when ] follows immediately the opening [

#### awk 显示最后一列

    awk '{print $(NF)}'
    
#### bash 命令输入几个技巧

    !!	最后一条命令
    !n	第n条命令
    !-n	倒数第n条命令
    !string	以string开始的最近一条命令
    !^	第一个参数
    !$	最后一个参数
    !*	除第一个命令之外的所有参数
    ^s1^s2	将上一条命令中的s1切换为s2
    !!:n-m	上一条命令的n-m个参数。
 
 #### date 
 
    date -s "-5 seconds"
    date -s "+5 seconds"
    date -s "-5 mins"
    date -s "+5 mins"
    date -s "-5 hours"
    date -s "+5 hours"

#### 怎么挂载debugfs

    mount -t debugfs none /sys/kernel/debug

#### 提起deb包中的文件

    dpkg-deb -x package.deb extract/
   
#### 对文本折行
 
    fold –s
    
#### grep 递归行号

    grep -rn "loosgood"  * 
    egrep  -o '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+'
    *  表示当前目录所有文件，也可以是某个文件名
    -r 递归查找，不fllow 软链接
    -R 递归查找，fellow 软链接
    -w 只匹配整个单词，而不是字符串的一部分
    
 
如果想严格匹配某个单词（不是匹配字串），则需要添加边界判断，一般可以两种方式：

    -w 参数
    grep "\blog_file\b" or grep "\<log_file\>"
    
这两种只会匹配log_file 而不会匹配mon_cluster_log_file
\<和\>是最长见的正则表达式的扩展，用来表示单词的开头和结尾，所谓的单词就是数字字母和下划线。
\b和类似，但是可以同时代表\<和\>。也就是说\b的两侧必须一侧是单词字符，一侧不是。
而\B表示的是\B两侧必须都是单词字符。所以一般\B匹配的就是某个单词字符串的子串。

\<，\>， \s，\w，\b这些很方便的表达都是GNU的扩展，而不是POSIX的标准。
这些扩展一般的GNU版本常常会支持，但是需要确认。更多见《shell脚本学习指南》

###### 查找man文档中以连字符开始的选项

    $ man chmod | grep [-]R
        -R, --recursive
 
#### gcc g++ 安装

    yum install gcc
    yum install gcc-c++

#### pylint 用法
    
    pylint --rcfile=conffile module.py      // 某模块
    pylint --rcfile=conffile packagename    // 某个包
    
#### readline 相关快捷键

    ctrl-a // 光标跳转到行头
    ctrl-e // 光标跳转到行尾
    esc-b // 往后移动一个词
    esc-f // 往前移动一个字符
    ctrl-b // 往后移动一个字符
    ctrl-f // 往前移动一个字符
    ctrl-u // 从光标位置删除到行头
    ctrl-k // 从光标位置删除到行尾
    ctrl-w // 往后删一个词
    esc-d // 往前删一个词
    ctrl-h // 往后删一个字符
    ctrl-d // 往前删一个字符
    ctrl-x ctrl-u // undo 回退
    ctrl-_ // 回退
    ctrl-y // 粘贴前一次通过ctrl-w或esc-d删除的词
    ctrl-t // 互换两个字符
    esc-t // 互换两个词
    ctrl-l // 清屏
    ctrl-j
    ctrl-g
    !!:/s/--old_option/--new_option/
    ctrl-v ctrl-j 多行编辑

#### 如何分割文件

    split
    
#### ssh-keygen中使用passphrase

ssh-keygen时如果输入passphrase那么在使用ssh的时候就会提示你输入passphrase。比如你在：

    git clone ssh://git@github.com/shaojwa/lang.git
    
同时如果你修改主机hostname原来的public key自然就不再有效。
 
#### ssh 常见登入问题

    ssh –v/-vv/-vvv	一个v显示debug1，两个v显示到debug2，类推，用于调试。

远程不允许登入问题

    /etc/ssh/sshd_config同时开启：    
    PermitRootLogn Without-password
    PermitRootLogn yes
    service ssh reload
    
登入延迟问题

    用ssh –vvv root@192.168.4.11调试查看延迟原因，
    如果是GSS失败，则设置/etc/ssh/sshd_config中的 GSSAPIAuthentication 为no，然后重启sshd
    
#### 常用压缩解压命令

    tar -cf vdbench.tar vdbench/
    tar -czf vdbench.tar.gz vdbench/
    tar –xf example.tar
    
#### tcpdump常用法

    -n：不将ip解析为域名
    -m: 全部显示port
    -X: 以ASCII 和 十六进制显示
    -i: tcpdump -i eth0
    -b: ip/arp/rarp
    -t: 不显示时间

    tcpdump host 10.99.68.34
    tcpdump –i em3
    tcpdump dst port not telnet
    tcpdump src host 192.168.0.1 and dst net 192.168.0.0/24
    tcpdump -i bond1  host 172.12.15.162 and port 6800


#### 怎么配置网络延时

    tc qdisc del  dev ethA08-0 root netem delay 5s
    tc qdisc add dev eth1 root netem delay 3s
    tc qdisc del dev eth1 root netem delay 3s
    tc qdisc show dev eth1
    
 ### vimdiff 常用命令
 
    vimdiff
    diffget
    diffput
    diffu[pdate]
    do //own
    dp //put
    ]c //next diff
    [c //prev diff
    zo
    zc
    
#### xargs常用法
    
    cat hosts | xargs -I{} ssh root@{} hostname
    sudo locate -br ^.*\\.sh$  | xargs -i bash -c 'echo {} >> total.sh; cat {} >> total.sh'

#### yum

    yum provides ifconfig
    yum whatprovides ifconfig
    yum install net-tools

#### 查看DNS服务器ip

    cat /etc/resolve.conf
    nmcli dev show | grep DNS

#### 在虚拟机中配置DNS服务

    IPADDR=192.168.245.128
    NETMASK=255.255.255.0
    GATEWAY=192.168.245.1
    DNS1=192.168.245.2
    
#### 清空dns缓存

    /etc/init.d/dns-clean
    
    
#### 服务重启过多导致无法再次重启

    man systemd.service
    man systemd.unit
    
* StartLimitIntervalSec 检查时间
* StartLimitBurst 启动次数
* systemctl reset-fail

案例： 

/opt/xxx/lib/systemd/system/ceph-mds@.service  

    StartLimitInterval=30min
    StartLimitBurst=3

    systemctl reset-failed ceph-mds@mds0.service
    systemctl reset-failed ceph-mds@target



#### 关闭防火墙

    firewall-cmd --state
    service firewalld status
    
    systemctl start firewalld.service
    service firewalld start
    
    systemctl stop firewalld.service
    service firewalld stop
    
    systemctl disable firewalld.service
    service firewalld disable
    
 #### selinx查询设置
 
 * 三种模式
 * 两种策略：targeted 和 strict
 * 查看状态
 
       sestatus -v
     
 * 查看当前模式
 
       getenforce
 * 设置成permissive 模式
 
       setenfroce 0
        
 * 持久化设置
 
       /etc/selinux/config