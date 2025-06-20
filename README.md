# Prometheus 網路監控專案

## 專案簡介

本專案以 **Docker Compose** 部署完整的網路監控解決方案，包含：
- **Prometheus**：指標資料收集
- **Grafana**：數據視覺化
- **SNMP Exporter**：網路設備監控
- **Node Exporter**：主機系統指標
- （可選）**Alertmanager**：告警管理（已預設註解）

---

## 目錄結構

```
.
├── docker-compose.yml         # 主要服務編排檔案
├── config/                    # 各服務設定檔
│   ├── prometheus/            # Prometheus 設定
│   ├── snmp_exporter/         # SNMP Exporter 設定
│   └── alertmanager/          # Alertmanager 設定
├── data/                      # 各服務資料目錄（已加入 .gitignore）
│   ├── grafana_data/          # Grafana 資料
│   ├── prometheus_data/       # Prometheus 資料
│   └── alertmanager_data/     # Alertmanager 資料
├── cutboard/                  # 暫存或其他檔案
└── README.md                  # 專案說明文件
```

---

## 快速啟動

1. **複製本專案到本地端**
   ```bash
   git clone <你的-repo-url>
   cd prometheus01
   ```

2. **啟動所有服務**
   * 請先進入 ./config/snmp_exporter 執行如下指令產生 snmp.yml，完成 snmp-exporter config
   ```bash
   make docker-generate
   ```

   * 啟動相關服務
   ```bash
   docker-compose up -d
   ```

3. **服務啟動後，透過瀏覽器存取：**
   - **Grafana**：[http://localhost:3000](http://localhost:3000)  
     預設帳號密碼：`admin` / `admin`（首次登入會要求修改密碼）
   - **Prometheus**：[http://localhost:9090](http://localhost:9090)
   - **SNMP Exporter**：[http://localhost:9116](http://localhost:9116)
   - **Node Exporter**：[http://localhost:9100](http://localhost:9100)（如有啟用）

---

## 注意事項

- **資料目錄（data/）已加入 `.gitignore`，不會被版本控制。**
- 請依需求調整 `config/` 內各服務設定檔。
- 若需啟用 Alertmanager，請取消 `docker-compose.yml` 內相關註解。
- 若遇權限問題，請確認 `data/` 目錄下各子目錄擁有者與權限設定正確（如 Grafana 須為 472:472）。

---

## 參考連結

- [Prometheus 官方文件](https://prometheus.io/docs/)
- [Grafana 官方文件](https://grafana.com/docs/)
- [SNMP Exporter](https://github.com/prometheus/snmp_exporter)
- [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/)

---

如需協助或有任何問題，歡迎提出！