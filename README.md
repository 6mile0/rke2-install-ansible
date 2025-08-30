# RKE2を構築するAnsible Playbook
master, worker1, worker2をそれぞれ構築できます

## 実行

### 依存関係をインストール
```bash
pip install -r requirements.txt
```
### Dry-Run
```bash
ansible-playbook -i inventory.ini playbook.yml --check
```

### 本番実行
```bash
ansible-playbook -i inventory.ini playbook.yml
```
