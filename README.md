octoprintインストール自動化
webcameraも設定

# インストール先の設定
armbianがインストール済みでネットワーク接続済みの前提
以下のように設定を追加して接続しやすくする

# 母艦側の設定
```
 scp ~/.ssh/id_rsa.pub m0a@192.168.11.111:/home/m0a/.ssh/authorized_keys
```

```~/.ssh/config
# orangepi
Host orangepi(192.168.11.111)
  HostName 192.168.11.111
  IdentityFile ~/.ssh/id_rsa
  User m0a
```



# octoprintインストール


```
ansible-galaxy install -p ./roles -r requirements.yml
ansible-playbook -i hosts playbook.yml
```

