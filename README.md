Got it 👍
Here is a **VERY SHORT, ONLY IMPORTANT, ONE-TIME COPY-PASTE README**
❌ No Mario app
❌ No extra theory
✅ Only what you actually did and need to remember

---

```markdown
# 📊 Prometheus & Grafana Monitoring with Email Alerting

## 🔹 What I Implemented

- Set up **Prometheus** and **Grafana** using Docker
- Created **custom dashboards** in Grafana
- Configured **CPU usage alerts**
- Integrated **real email alerting using Gmail SMTP**
- Tested alerts by generating CPU load

---

## 🛠️ Tools Used

- Docker & Docker Compose
- Prometheus
- Node Exporter
- Grafana
- Gmail SMTP (App Password)

---

## 📈 Monitoring Setup

- **Prometheus** collects system metrics
- **Node Exporter** exposes CPU, memory, disk, and network metrics
- **Grafana** visualizes metrics using dashboards
- Prometheus added as data source using:
```

[http://prometheus:9090](http://prometheus:9090)

```

---

## 🚨 Alert Configuration

- Alert Type: **CPU Usage**
- Condition: **CPU > 80%**
- Evaluation Interval: **1 minute**
- Pending Period: **1 minute**
- Alert States:
```

Normal → Pending → Firing

````

Alert tested using:
```bash
stress --cpu 4 --timeout 180
````

---

## 📧 Email Alerting (Gmail SMTP)

* Grafana cannot send emails by itself
* Configured **Gmail SMTP** to send alerts
* Enabled **2-Step Verification** on Gmail
* Generated **App Password** for Grafana
* Used SMTP details:

  ```
  SMTP Server: smtp.gmail.com
  Port: 587
  Encryption: STARTTLS
  ```

### Result

✅ **Alert email successfully received in Gmail inbox**

---

## 🧠 Key Concepts Learned

* Grafana requires an **SMTP server** to send email alerts
* **Port 587** is used for secure, authenticated SMTP
* App Password is required instead of normal Gmail password
* Alerts must be tested before using production thresholds
* Persistent storage is required in Grafana to retain dashboards and alerts

---

## ✅ Current Status

✔ Metrics collection working
✔ Dashboards created
✔ CPU alert firing correctly
✔ **Real email alert received successfully**

---

## 📌 Final Update

Successfully implemented monitoring and alerting using Prometheus and Grafana.
CPU alert was triggered and **email notification was delivered using Gmail SMTP**, validating the complete setup.

