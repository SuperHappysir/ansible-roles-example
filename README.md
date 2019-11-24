### 安装Ansible
```bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-6.repo
yum install ansible --nogpgcheck -y &> /dev/null && echo success
```

### clone 项目
```bash
git clone https://github.com/SuperHappysir/ansible-roles-example.git /etc/ansible/roles/
```

### 使用demo剧本进行测试
```bash
# copy 公钥到目标主机（有多少个目标主机需要复制多少次）
ssh-copy-id -i /root/.ssh/id_rsa.pub root@目标主机ip

cd /etc/ansible/

# 编辑host清单组信息
vim roles/install-golang/demo/group_vars/install-golang-env

# 使用角色install-golang下定义的demo变量和剧本进行go环境安装
ansible-playbook -i roles/install-golang/demo/group_vars/install-golang-env roles/install-golang/demo/install-golang.yml
```

### 自己编写剧本调用role
```bash
cd /etc/ansible
vim xxxx.yml

# 输入保存
- hosts: "host-group"
  remote_user: root # 以root用户操作
  roles:
    - xxx
    
ansible-playbook xxxx.yml
```
