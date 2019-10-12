一.关于ubuntu开机自启动的说明:
-
ubuntu18.04不再使用 inited 管理系统，改用 systemd
但是个人认为开机启动的rc.local更加好用，所以可以自己配置rc.local
1.实现原理<br>
systemd 默认会读取 /etc/systemd/system 下的配置文件，该目录下的文件会链接 /lib/systemd/system/ 下的文件。一般系统安装完 /lib/systemd/system/ 下会有 rc-local.service 文件，即我们需要的配置文件.<br>
2.将 /lib/systemd/system/rc-local.service 链接到 /etc/systemd/system/ 目录下面,分别执行如下命令

    	ln -fs /lib/systemd/system/rc-local.service /etc/systemd/system/rc-local.service
修改文件内容

     sudo vim /etc/systemd/system/rc-local.service
 在文件末尾增加
    
      		[Install]
		WantedBy=multi-user.target
		Alias=rc-local.service
创建/etc/rc.local文件并编辑

    	   sudo touch /etc/rc.local
               sudo vim /etc/rc.local


上述操作需要注意获取文件权限,最后在rc.local文件中可以直接编写想要执行的命令或者脚本文件(编写位置在exit 0之前)

    #!/bin/sh -e  
    #  
    # rc.local  
    #  
    # This script is executed at the end of each multiuser runlevel.  
    # Make sure that the script will "exit 0" on success or any other  
    # value on error.  
    #  
    # In order to enable or disable this script just change the execution  
    # bits.  
    #  
    # By default this script does nothing.  

    exit 0  


    
