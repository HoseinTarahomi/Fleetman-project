# 🚀 Fleetman DevOps Project

پروژه‌ی **Fleetman** یک پیاده‌سازی کامل از فرآیند **CI/CD در محیط DevOps** است که با استفاده از GitLab، Harbor، ActiveMQ و Kubernetes اجرا شده است.
هدف این پروژه، شبیه‌سازی چرخه‌ی کامل توسعه، استقرار و اجرای یک سیستم مبتنی بر میکروسرویس‌ها در محیط واقعی است.

---

## 🧩 اجزای پروژه

* **Kubernetes** → برای ایجاد و مدیریت کلاستر و اجرای سرویس‌ها
* **GitLab** → برای مدیریت سورس کد و اجرای Pipelineهای CI/CD
* **Harbor** → به عنوان Image Registry خصوصی جهت ذخیره‌ی Docker Imageها
* **ActiveMQ** → به عنوان Message Broker برای ارتباط بین سرویس‌ها

*(ابزارهایی مانند Rancher، ArgoCD، Prometheus، Grafana و ELK Stack در فاز بعدی پروژه اضافه خواهند شد.)*

---

## ⚙️ نحوه‌ی عملکرد پروژه

1. سورس‌کد و Dockerfile هر سرویس در GitLab قرار دارد.
2. GitLab Runner (نوع Shell) وظیفه‌ی **Build** ایمیج‌ها و **Push** آن‌ها به Harbor را دارد.
3. پس از پایان Build، مرحله‌ی **Deploy** آغاز می‌شود:

   * در این مرحله GitLab Runner از نوع Kubernetes، فایل‌های Manifest (Deployment، Service و ...) را از Repository کلون کرده و درون کلاستر اعمال می‌کند.
4. سرویس ActiveMQ به عنوان Message Broker بین دو اپلیکیشن Fleetman عمل می‌کند تا ارتباط بین microserviceها برقرار شود.

---

## 🧱 ساختار کلی پروژه

```
fleetman/
├── manifests/        # فایل‌های YAML مربوط به Kubernetes
├── ci-cd/            # فایل‌های pipeline مربوط به GitLab
├── harbor/           # تنظیمات مربوط به Image Registry
├── src/              # سورس‌کد سرویس‌ها و Dockerfileها
└── README.md         # مستندات پروژه
```

---

## 🚀 نحوه‌ی اجرا

برای استقرار پروژه در کلاستر:

```bash
kubectl apply -f manifests/
```

برای اجرای pipeline در GitLab، کافی است Commit جدید انجام دهید تا مراحل **Build → Push → Deploy** به‌صورت خودکار اجرا شوند.

---

## 📘 توضیحات تکمیلی

* این پروژه به‌صورت آموزشی طراحی شده تا چرخه‌ی کامل DevOps از Build تا Deployment را در محیط واقعی نمایش دهد.
* تمامی ایمیج‌ها در **Harbor Private Registry** ذخیره می‌شوند.
* در مراحل بعدی، ابزارهای مانیتورینگ و لاگ‌گیری (Prometheus, Grafana, ELK Stack) نیز به پروژه اضافه خواهند شد.

---

