ѡ��ϵͳ����ĵ�
=============
## **ID��ʽ**  
#### userID
- 9λ���� ( char(9) )
- ��һλ��0����ʦ 1,2,3,4����һ�����������������
- �м���λԺϵID  
- ����λ��ˮ��

#### �γ�ID
- 6λ
- ��ʼ100000
- ��ˮ�ţ���ʵ������

## **��¼����** 

- �����˺ţ�ѧ�š���ְ���ţ������루md5���ܣ�  
- ֧�ֵ�¼��ע�ᣬ��������

## **��������**
- �����˺ţ�����
- ����ȷ����д������

## **ע�����**  

#### ѧ��ע��  
- ѧ������
- ����
- �ٴ���д����
- ����ѧԺ
- �꼶    
  
#### ��ʦע��
- ����
- ����
- �ٴ���������
- ����ѧԺ
- (�꼶һ��ǿ��Ϊ0)


## **ѧ������**  
- (ģ��ѧУѡ��ϵͳ)���Ϸ��Ϸ��γ̱�
- ���·�ΪѧУ�γ���¼(ÿҳ��ʾ10�����ɷ�ҳ)
- ѡ������ģ��ƥ��  
- ���Ϊѧ��������Ϣ���꼶��������ѧ�ţ�����ѧԺ��


## **��ʦ����**
- ���Ϊ��ʦ������Ϣ
- ���Ϸ�Ϊ����Ŀγ�
- ���·�Ϊ����γ�ѡ�ε�ѧ����ѧ�ţ�������
- ����ӿγ�ѡ�ȡ���γ�ѡ��

### ��ӿγ̽���  
- �γ���
- ��������
- �γ̽��� (������ɺ���������õĿ���ʱ��)
- ����ʱ�� (�ɶ�ѡ)
- �γ�ѧ��
- (�γ�ID�Զ�����)
- ѡ�γɹ��������ʾ����

### ȡ���γ̽���
- ����ѯ�ʴ���
- ִ�����ݿ����

## **���ݿ����**
```sql
create table department
(
	did char(4), 
	dname varchar(30),
	primary key(did)
);
create table user
(
	id char(9),
	name varchar(30),
	grade int,            
	did char(4),
	pwd varchar(30),
	primary key(id),
	foreign key(did) references department(did)
);
create table room
(
	rid char(4),
	monday char(11),
	tuesday char(11),
	wednesday char(11),
	thursday char(11),
	friday char(11),
	saturday char(11),
	sunday char(11),
	primary key(rid)
);
create table course
(
	cid char(6),
	cname varchar(30),
	current int,
	max int,
	tid char(9),
	ctime char(3),#"122"������һ�ڶ��ڿ�ʼ������ʱ
	rid char(4),
	credit int,
	primary key(cid),
	foreign key(tid) references user(id),
	foreign key(rid) references room(rid)
);
create table sc
(
	sid char(9),
	cid char(6),
	primary key(sid,cid),
	foreign key(sid) references user(id),
	foreign key(cid) references course(cid)
);

```
## **ѡ������**  

��һ��ѡ��
- ѧ��ֻ��ѡ��Ժϵ�����꼶�γ�  

�ڶ���ѡ��  
- ѧ����ѡ����Ժϵ�������꼶�γ�
- ����������

## **�����������**  
#### ��¼
����
```json
{
    "pid":1,
    "user":"200010001",
    "pwd":"asdffgghhj"
}
```

����  
```json
{
    "state":true
}
```

#### ע��
����
```json
{
    "pid":2,
    "name":"Tom",
    "did":"0001",
    "grade":2,
    "pwd":"asdfghj"
}
```

����
```json
{
    "user":"200010001"
}
```

#### ��������
����
```json
{
    "pid":3,
    "user":"200010001",
    "name":"Tom",
    "pwd":"newpwd"
}
```
����
```json
{
    "state":true
}
```

#### ����ѧԺ
����
```json
{
    "pid":4
}
```
����
```json
[
    "0001.�����",
    "0002.��ѧ"
]
```

#### ����ѧ���γ̱���Ϣ
����  
```json
{
    "pid":5,
    "user":100010001
}
```
����
```json
[
   {
        "cid":"000101",
        "cname":"�������",
        "rid":"2108",
        "ctime":"112",
        "tname":"�"
   },
   {
        "cid":"000101",
        "cname":"���ݿ�",
        "rid":"2108",
        "ctime":"112",
        "tname":"�"    
   }
]
```
####  �鿴��ѡ�γ�  
����  
֧��ģ��ƥ��   
δѡ�γ̹��࣬ÿҳ��ʾ10���γ̣�index��ʾҳ��,ÿҳ10������
```json
{
    "pid":6,
    "index":0,
    "user":"100010001",
    "cname":"",
    "cid":"",
    "tname":""
}
```
����  
total��ʾ���д�ѡ�ɿγ̣��������ҳ����
```json
{
    "total":98,
    "courses":
    [
        {
            "cid":"000101",
            "cname":"�������",
            "current":15,
            "max":45,
            "rid":"2108",
            "ctime":"112",
            "tname":"�",
            "credit":2
        },
        {
            "cid":"000102",
            "cname":"���ݿ�",
            "current":15,
            "max":45,
            "rid":"2108",
            "ctime":"112",
            "tname":"�",
            "credit":2     
        }
    ]
}
```
#### ѧ��ѡ�β���
����  
```json
{
    "pid":7,
    "user":"100010001",
    "cid":"000302"
}
```
����  
```json
{
    "state":true
}
```

#### ѧ���˿β���
```json
{
    "pid":8,
    "user":"100010001",
    "cid":"000302"
}
```
����  
```json
{
    "state":true
}
```
����
```sql
delete from sc where sid="100010001" and cid="000302"
```

#### ��ʦ��ӿγ� 
����
```json
{
    "pid":9,
    "user":000010001,
    "cname":"�������",
    "rid":"2109",
    "ctime":"312",
    "max":45,
    "credit":2
}
```
����
```json
{
    "state":true,
    "cid":"000101"
}
{
    "state":false
}
```

#### ��ʦɾ���γ�
����  
```json
{
    "pid":10,
    "cid":"000101",
    "user":"000010001"
}
```
����  
```json
{
    "state":true
}
{
    "state":false
}
```
#### �������н���ռ�����
����  
```json
{
    "pid":14,
    "rid":"2108"
}
```
����  
�߸��ַ������������һ�����յĽ�ʦռ�����  
��һ��������,��nλ�����n-1�ڿε�ʹ�����
```json
[
    "01100000000",
    "01100000000",
    "00000000000",
    "00110000000",
    "00000000000",
    "00000000000",
    "00000000000",
]
```

#### �����û���Ϣ
����
```json
{
    "pid":13,
    "user":100010001
}
```
����
```json
{
    "dname":"�����ѧԺ",
    "name":"�",
    "round":1
}
```
#### ��ʦ�鿴�Լ�����Ŀγ�  
����
```json
{
    "pid":11,
    "user":"0000010001"
}
```
����
```json
[
        {
            "cid":"000101",
            "cname":"�������",
            "current":15,
            "max":45,
            "rid":"2108",
            "ctime":"112",
            "credit":2
        },
        {
            "cid":"000102",
            "cname":"���ݿ�",
            "current":15,
            "max":45,
            "rid":"2108",
            "ctime":"112",
            "credit":2     
        }
]
```
#### ��ʦ�鿴ѡ���Լ��γ̵�ѧ��  
����
```json
{
     "pid":12,
     "cid":"000101"   
}
```
����
```json
[
    {
        "id":"100010001",
        "name":"�",
        "grade":1,
        "dname":"�����ѧԺ"
    },
    {
        "id":"100010002",
        "name":"�",
        "grade":1,
        "dname":"�����ѧԺ"
    }
]
```

#### ��������б�
����
```json
{
    "pid":15
```
����
}
```json
[
    "2018","2014","2001"
]
```
## **����ӿ�**   
ÿ�ε���send��������recv����

```c++
bool send(const QJsonObject &);//����
QJsonDocument recv();//����
```
