
return "asd%s%d"%("oooo",4)#asd"oooo"4

�ַ�����split()��JavaScriptһ��һ����,���ַ����ָ�Ϊlist


":".join(list)#���JavaScript���ǲ�һ������������


2.7��
f.file('file.txt','[a|w|r|a+]')
file()�����ȼ���open()����

try:
    f=open('123.txt')
    f.read()
    print(f)
except:
    f.open("write.text")
    f.read()
    f.close()
    print(f)

from random inport randint
random.randint(1,10)#1��10֮��������
random.choice([...])#�����list��ѡһ��

p=[1,2,4,3,5]

2 in p//True
p.index(5)//4
2 not in p //True
not 2 in p//True

x,y,z
x=x+y  --1
y=x+y+1  --2
z=2y+2x+1  --3
