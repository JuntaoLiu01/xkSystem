����˰�װ�ĵ�
======


##����Ҫ��  
- python 3.5 or newer   
- pip  
- mysql  

##���Ի���  
Ubuntu

##��װ
###step1
```bash
git clone https://github.com/hzshang/xkSystem.git
cd xkSystem/server
```  
###step2
�������ݿⲢ����sqlĿ¼�µ�struct.sql�ļ�  
###step3
��װpythonģ��cymysql
```bash
pip3 install cymysql
```
###step4
����sample-config.json��������Ϊconfig.json,�޸Ĳ���  
```json
{
	"db_host":"yourHost",//���ݿ��ַ 
	"db_database":"database",//���ݿ�����
	"db_user":"user",//user
	"db_passwd":"passwd",//password
	"listen":"0.0.0.0",//������ַ
	"port":3307,//�����˿�
	"round":1//ѡ������
}
```
###step5
�޸�MTU  
���ڵ��η��͵����ݰ�����Ӧ��MTU(һ�����ݰ�������ֽ���)��Ϊ4096  
```bash
#�鿴MTU  
cat /sys/class/net/eth0/mtu
#�޸�MTU  
echo "4096" > /sys/class/net/eth0/mtu  
#��������ʹ�޸���Ч
/etc/init.d/networking restart
```

##����
```bash
python3 server.py
```
��̨����  
```bash
./run.sh 
```
ֹͣ
```bash  
./stop.sh
```
����
```bash  
./restart.sh
```