# OpenShift 4'te Kubelet Down Durumunda Troubleshooting

Bu depo, OpenShift 4 üzerinde kubelet'in down olması durumunda nasıl troubleshooting yapılacağını ve quota hatalarının nasıl çözüleceğini açıklar.

## Senaryo

1. **Node'ların Durumunu Kontrol Etme**:
   - `oc get nodes --output wide` komutu ile node'ların durumunu kontrol edin.
   - `NotReady` durumundaki node'ları tespit edin.

2. **Node Üzerinde Debug Pod'u Başlatma**:
   - `oc adm debug node/<node-name>` komutu ile node üzerinde debug pod'u başlatın.

3. **Kubelet Durumunu Kontrol Etme**:
   - Debug pod'unda `systemctl status kubelet` komutu ile kubelet'in durumunu kontrol edin.
   - Eğer kubelet durmuşsa, `systemctl start kubelet` komutu ile yeniden başlatın.

4. **Kubelet Loglarını İnceleme**:
   - `journalctl -u kubelet -f` komutu ile kubelet loglarını inceleyin.

5. **Container Listeleme ve Logları İnceleme**:
   - `oc get pods -n <namespace>` ile container'ları listeleyin.
   - `oc logs <pod-name> -n <namespace>` ile container loglarını görüntüleyin.

6. **Quota Hatası ve Çözümü**:
   - Quota hatası alıyorsanız, `oc get quota --all-namespaces | grep my-quota` komutu ile quota'ları kontrol edin.
   - Pod'larınızın `requests` ve `limits` değerlerini güncelleyerek hatayı çözün.

## Örnek Komutlar

- Node'ları listeleme:
  ```bash
  oc get nodes --output wide
