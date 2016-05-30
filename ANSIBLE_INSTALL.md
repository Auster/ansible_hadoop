### ansible install
```sh
wget https://bootstrap.pypa.io/get-pip.py && \
python ./get-pip.py && \
yum install -y gcc python-devel libffi-devel openssl-devel && \
pip install paramiko PyYAML Jinja2 httplib2 six && \
pip install ansible
```
