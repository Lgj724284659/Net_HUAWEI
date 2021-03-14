import paramiko
import time

ip = "192.168.1.254"
user = "huawei"
pw = "huawei@123"

#欢迎关注喜欢华为的李工
ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect(hostname=ip, username=user , password=pw)


print("恭喜您成功登录到ensp上的交换机了！" , ip)

#连接成功后，调用invoke_shell（）方法来唤醒shell，也就是华为系统命令行，同时把它赋值给command，方便后续调用。
command = ssh.invoke_shell()

#向设备发送命令，需要执行的命令。
command.send("system\n")
command.send("vlan 20\n")
command.send("quit \n")
command.send("int vlan 20 \n")
command.send("ip add 192.168.20.1 24 \n")
command.send("vlan 30\n")
command.send("quit \n")
command.send("int vlan 30 \n")
command.send("ip add 192.168.30.1 24 \n")
command.send("vlan 40\n")
command.send("quit \n")
command.send("int vlan 40 \n")
command.send("ip add 192.168.40.1 24 \n")
command.send("vlan 50\n")
command.send("quit \n")
command.send("int vlan 50 \n")
command.send("ip add 192.168.50.1 24 \n")
command.send("vlan 60\n")
command.send("quit \n")
command.send("int vlan 60 \n")
command.send("ip add 192.168.60.1 24 \n")
command.send("quit \n")
#欢迎关注喜欢华为的李工
#使用sleep函数，让脚步执行后休息2s，再回显内容。65535是回显多少个字符
time.sleep(2)
output = command.recv(65535)
print(output.decode("ascii"))

#配置完后，用close方法退出ssh  
ssh.close()     
