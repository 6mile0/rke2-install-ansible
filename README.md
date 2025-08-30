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

### rke2-ingress-nginx-controllerが上がってこないとき
#### ▶ 次のようなエラーが出る場合
```bash
 Warning  FailedCreatePodSandBox  116s (x16 over 2m11s)  kubelet            (combined from similar events): Failed to create pod sandbox: rpc error: code = Unknown desc = failed to setup network for sandbox "428699b7c25410de94995fd92006fc74d56e7c6333333102706a94e54c2cae52": plugin type="portmap" failed (add): failed to open iptables: exec: "iptables": executable file not found in $PATH
```
素直にiptable入れて再起動すると治る

#### ▶ IPの割当に失敗している場合
```bash
plugin type='calico' failed (add): failed to allocate for range 0: no IP addresses available in range set: 10.42.5.1-10.42.5.254."
```

以下を実行して再起動すると治る
```bash
rm -rf /var/lib/cni/networks/k8s-pod-network
```

ref: https://github.com/rancher/rke2/issues/4385
