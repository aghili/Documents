# داکیومنت مهاجرت محک از Delphi به .NET  
**WPF + MVVM + EF Core + سامانه مودیان**  
**نسخه:** 1.5 (کامل و بهینه برای گیت‌هاب)  
**تاریخ:** ۱۲ آذر ۱۴۰۴  

---

## هدف پروژه
بازنویسی کامل نرم‌افزار حسابداری محک از Delphi به .NET 8 با معماری مدرن:
- UI: WPF + MVVM  
- دیتابیس: EF Core Code-First  
- ادغام: سامانه مودیان (کامل)  
- معماری: Clean Architecture / Modular Monolith  

---

## محدوده (Scope)
| سری      | سطوح         | قالب‌ها                     |
|----------|--------------|-----------------------------|
| عمومی   | ۱، ۲، ۳      | فروشگاهی – شرکتی – صنفی   |
| تجاری   | ۱ تا ۵       | فروشگاهی – شرکتی – تولیدی   |

---

## لیست Views (WPF)

| # | View                              | توضیحات کلیدی                                    | سطح          |
|---|-----------------------------------|--------------------------------------------------|--------------|
| 1 | `MainDashboardView`               | داشبورد + وضعیت مودیان                           | همه          |
| 2 | `InitialSetupWizardView`          | تنظیمات اولیه + تنظیمات مودیان                  | همه          |
| 3 | `InvoiceView`                     | فاکتور + دکمه «ارسال به مودیان»                | همه          |
| 4 | `TransactionView`                 | دریافت/پرداخت، چک، تنخواه                      | همه          |
| 5 | `InventoryManagementView`         | انبار، سریال، رنگ/سایز + شناسه کالا            | همه          |
| 6 | `POSView`                         | فروش همزمان + ارسال realtime به مودیان         | عمومی ۳ / تجاری ۱+ |
| 7 | `ReportsDashboardView`            | گزارشات + تاریخچه مودیان                        | همه          |
| 8 | `AccountingDocumentView`          | اسناد دستی/گروهی، تراز، دفاتر، کدینگ درختی     | همه          |
| 9 | `ModianIntegrationView`           | تنظیمات مودیان، کارپوشه، رفع خطا               | همه          |
|10 | `PayrollView`                     | حقوق و دستمزد                                   | تجاری ۳+     |
|11 | `ProductionView`                  | فرمول تولید، بهای تمام‌شده                     | تجاری ۲+     |
|12 | `ProjectView`                     | پروژه و مراکز هزینه                             | تجاری ۴+     |


---

## سرویس‌های اصلی

| سرویس                         | وظیفه اصلی                                      | سطح          |
|-------------------------------|------------------------------------------------|--------------|
| `InvoiceService`              | تخفیفات + تولید JSON/XML + ارسال به مودیان     | همه          |
| `AccountingService`           | ثبت خودکار سند، تراز، دفاتر                    | همه          |
| `ModianIntegrationService`    | ارسال/استعلام/رفع خطا (retry + Polly)         | همه          |
| `DocumentManagementService`   | بایگانی اسناد، لینک به فاکتور/چک               | همه          |
| `ReportService`               | گزارشات + خروجی قانونی + گزارش مودیان         | همه          |

---

## زمانبندی پروژه (۵۰ هفته)

| فاز | محتوا                                   | شروع       | پایان      | مدت  |
|-----|-----------------------------------------|------------|------------|------|
| 1   | داشبورد + فاکتور پایه                  | ۱۴۰۴/۱۰/۱۱ | ۱۴۰۴/۱۲/۰۸ | ۸ هفته |
| 2   | انبار و موجودی                          | ۱۴۰۴/۱۱/۲۵ | ۱۴۰۵/۰۱/۱۲ | ۶ هفته |
| 3   | خزانه‌داری و چک                        | ۱۴۰۴/۱۲/۲۵ | ۱۴۰۵/۰۲/۱۰ | ۵ هفته |
| 4   | حسابداری و اسناد کامل                   | ۱۴۰۵/۰۱/۱۲ | ۱۴۰۵/۰۳/۱۰ | ۷ هفته |
| 5   | ادغام سامانه مودیان                    | ۱۴۰۵/۰۲/۲۵ | ۱۴۰۵/۰۴/۱۰ | ۶ هفته |
| 6   | گزارشات + خروجی قانونی                 | ۱۴۰۵/۰۳/۲۵ | ۱۴۰۵/۰۴/۲۵ | ۴ هفته |
| 7   | حقوق، تولید، پروژه                     | ۱۴۰۵/۰۴/۱۰ | ۱۴۰۵/۰۶/۱۰ | ۸ هفته |
| 8   | امکانات پیشرفته + تست نهایی + استقرار   | ۱۴۰۵/۰۵/۲۵ | ۱۴۰۵/۰۷/۲۵ | ۶ هفته |


---

## دیاگرام‌ها

### Class Diagram (معماری کلی)
![Class Diagram](./puml/class_diagram.puml)

### Sequence – ارسال فاکتور به مودیان
![Sequence Modian](./puml/sequence_moadian.puml)

### Sequence – ثبت خودکار سند حسابداری
![Sequence Document](./puml/sequence_document.puml)

### ER Diagram (بخش کلیدی)
![ER Diagram](./puml/er_diagram.puml)

### Component Diagram
![Component Diagram](./puml/component_diagram.puml)

### Deployment Diagram
![Deployment Diagram](./puml/deployment_diagram.puml)

### Deployment Diagram
![Activity Diagram](./puml/deployment_diagram.puml)

---

## ابزارها و کتابخانه‌ها

| دسته            | ابزار پیشنهادی                              |
|-----------------|---------------------------------------------|
| UI              | MaterialDesignInXaml یا MahApps.Metro       |
| گزارشات        | FastReport .NET (بهترین برای فارسی)        |
| چارت           | LiveCharts2                                 |
| DI & Logging    | Microsoft.Extensions + Serilog              |
| تست            | xUnit + Moq                                 |
| ادغام مودیان   | HttpClient + Polly + Newtonsoft.Json        |
| امنیت          | SecureStorage (توکن مودیان)               |

---

## ساختار پیشنهادی پروژه
src/
├── Mahak.UI/                  (WPF Views + ViewModels)
├── Mahak.Application/         (Services + Interfaces)
├── Mahak.Domain/              (Entities)
├── Mahak.Infrastructure/      (EF Core + Repositories)
├── Mahak.ModianIntegration/   (سرویس مودیان)
├── Mahak.Accounting/          (اسناد و حسابداری)
└── Mahak.Tests/


---

## وضعیت فعلی (دسامبر ۲۰۲۵)
- تحلیل اولیه انجام شده  
- دیاگرام‌ها طراحی شده  
- زمانبندی تخمین زده شده

---
