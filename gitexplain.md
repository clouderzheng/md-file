##explain how to use github
####register in https://github.com 
####create a project in your repository
####install a github server in your computer
    windows�û������� http://msysgit.github.com/

    mac�û������� http://code.google.com/p/tortoisegit/

    һ·next����װ�ɹ��� �ص�C�̣����κ��ļ����£�������Ҽ�����һЩ�˵�
    �� Git Init Hear��Git Bash��Git Gui �� ˵����װ�ɹ���

###����Git
    �������ڵ���Ӳ������һ��ط���ű��زֿ⣬�������ǰѱ��زֿ⽨����C:\MyRepository\1ke_test�ļ�����

    ����1ke_test�ļ��� ����Ҽ��������²��裺

    1���ڱ��زֿ����Ҽ�ѡ��Git Init Here��������һ��.git�ļ��У���ͱ�ʾ����git�����ɹ���
    2)�Ҽ�Git Bash����git������
###Ϊ�˱��������������ִ��git init����
    $ git init
###Ϊ�˰ѱ��صĲֿ⴫��github������Ҫ����ssh key��
    $ ssh-keygen -t rsa -C "your_email@youremail.com"
    �����your_email@youremail.com��Ϊ������䡣�ҵ�������343070065@qq.com��Ҳ����github��ע����Ǹ����䣺
    ֱ�ӵ�س���˵������Ĭ���ļ�id_rsa������ssh key�� 
    Ȼ��ϵͳҪ���������룬ֱ�Ӱ��س���ʾ��������
    �ظ�����ʱҲ��ֱ�ӻس���֮����ʾ��shh key�Ѿ����ɳɹ�
    Ȼ�����ǽ�����ʾ�ĵ�ַ�²鿴ssh key�ļ��� �ҵĵ��Եĵ�ַ��C:\Users\Administrator\.ssh ������Administrator���ҵĵ��Ե�����
    ��id_rsa.pub�����������key�������key��һ�Կ��������ַ�������ϣ����ù�����ֱ�Ӹ��ơ�
    �ص�github��վ������Account Settings�����ѡ��SSH Keys��Add SSH Key,
    title����ճ��key��
###3����֤�Ƿ�ɹ�����git bash������
    $ ssh -T git@github.com
    �س��ͻῴ����You��ve successfully authenticated, but GitHub does not provide shell access ����ͱ�ʾ�ѳɹ�����github��
###4������������Ҫ���ľ��ǰѱ��زֿ⴫��github��ȥ���ڴ�֮ǰ����Ҫ����username��email����Ϊgithubÿ��commit�����¼����
    $ git config --global user.name "your name"
    $ git config --global user.email "your_email@youremail.com"
###�ύ�ϴ�
    1���������ڱ��زֿ������һЩ�ļ�������README

    �ڱ����½�һ��README�ļ�  
    $ git add README

    $ git commit -m "first commit"
    2���ϴ���github 
    $ git push origin master

###