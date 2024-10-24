# これはなに
- ZabbixでNSDの統計情報を取得できるようにしたテンプレートです
- あと、自分用の備忘録

# 動作確認済みの環境
- Zabbix-Server: 7.0.5
- NSD: 4.3.8

# 設定方法
## 準備
### NSDの準備
- NSDのリモートコントロールが有効な状態になっていること
```
remote-control:
        control-enable: yes
        control-interface: 127.0.0.1
```
- 下の証明書と秘密鍵にZabbix-agentからアクセスできるように権限を設定する  
(権限は読み込みと書き込みがついていればいいはず)
```
・nsd_control.key
・nsd_control.pem
・nsd_server.key
・nsd_server.pem
```

### Zabbixの準備
- (前提)公式を参考にZabbix-agent2がインストールされて、Zabbixサーバからagentの情報が参照できる状態になっていること
- zabbix_agent2.confに下記を追記する
```
AllowKey=system.run[nsd-control stats]
```

## テンプレートの有効化
- ```nsd_zbx_template.yaml```をインポートする
- 対象ホストにテンプレートをアサインする

# 最後に
- 動作は確認しましたが、保証はしませんのであしからず
- 改善点などあればIssue等であげていただけるとうれしいです
