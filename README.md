# 🚀 پروژه Fleetman DevOps

پروژه‌ی **Fleetman** یک پیاده‌سازی جامع از فرآیند **CI/CD در محیط DevOps** است که با استفاده از ابزارهایی مانند **GitLab**, **Ansible** ,**Harbor**, **ActiveMQ** و **Kubernetes** اجرا شده است.
هدف این پروژه، شبیه‌سازی چرخه‌ی کامل توسعه، استقرار و اجرای یک سیستم مبتنی بر **میکروسرویس‌ها** در محیط واقعی است.

---

## 🧩 اجزای اصلی پروژه

* **Kubernetes** → برای ایجاد و مدیریت کلاستر و اجرای سرویس‌ها
* **GitLab** → برای مدیریت سورس‌کد و اجرای Pipelineهای CI/CD
* **Harbor** → به عنوان Image Registry خصوصی جهت ذخیره‌ی Docker Imageها
* **ActiveMQ** → به عنوان Message Broker برای ارتباط بین سرویس‌ها
* **Ansible** → برای نصب و اجرای Harbor

> *(در فازهای بعدی پروژه، ابزارهایی مانند ، ArgoCD، Prometheus، Grafana و ELK Stack نیز افزوده خواهند شد.)*

---

## ⚙️ نحوه‌ی عملکرد پروژه

1. سورس‌کد و Dockerfile هر سرویس در GitLab قرار دارد.
2. **GitLab Runner** (نوع Shell) مسئول **Build** ایمیج‌ها و **Push** آن‌ها به **Harbor** است.
3. پس از پایان مرحله‌ی Build، مرحله‌ی **Deploy** آغاز می‌شود:

   * در این مرحله **GitLab Runner (نوع Kubernetes)** فایل‌های Manifest (Deployment، Service و ...) را از Repository دریافت کرده و روی کلاستر اعمال می‌کند.
4. سرویس **ActiveMQ** به عنوان Message Broker بین اپلیکیشن‌های Fleetman عمل می‌کند تا ارتباط بین microserviceها برقرار شود.

---

## 🧱 ساختار کلی پروژه

```
fleetman/
├── manifests/        # فایل‌های YAML مربوط به Kubernetes
├── ci-cd/            # فایل‌های pipeline مربوط به GitLab
├── ansible/           # تنظیمات مربوط به نصب و اجرای Harbor
├── apps/              # سورس‌کد سرویس‌ها و Dockerfileها
└── README.md         # مستندات پروژه
```

---

## 🚀 نحوه‌ی استقرار و اجرا

### 📦 استقرار در Kubernetes

برای استقرار سرویس‌ها در کلاستر Kubernetes:

```bash
kubectl apply -f manifests/
```

### ⚙️ اجرای Pipeline در GitLab

با هر Commit جدید در Repository، مراحل زیر به‌صورت خودکار اجرا می‌شوند:

```
Build → Push → Deploy
```

---

## 📘 نکات تکمیلی

* این پروژه به‌صورت آموزشی طراحی شده تا چرخه‌ی کامل **DevOps** از مرحله‌ی Build تا Deployment را در محیط واقعی شبیه‌سازی کند.
* تمامی ایمیج‌ها در **Harbor Private Registry** ذخیره می‌شوند.
* در نسخه‌های بعدی، ابزارهای **مانیتورینگ (Prometheus, Grafana)** و **لاگ‌گیری (ELK Stack)** نیز به پروژه افزوده خواهند شد.

---

> 🧠 هدف اصلی Fleetman، درک عملی مفاهیم CI/CD، آشنایی با استقرار میکروسرویس‌ها در Kubernetes و کار با ابزارهای DevOps در یک محیط واقعی است.
