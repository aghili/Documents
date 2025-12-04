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
<div align="Center"> 

![Class Diagram](https://www.plantuml.com/plantuml/svg/RL5DRnCn4BtxLunoeGW5mOK31zGe0JKeaI8IaGDmc7WdkzPwFIjxd58X_ZlUnBJUDhViUo_lmtCR1Bt4pgfNyFujt9cwcQxeH1Rc5aE0XS7QOwSi7GM4mIU1G6KyQJ7iL6YDwp4fe6F7kl7S4OYFL32XmOhlZQlXY3QKZEEA0lNmuLq1UdHj1bMFkiMQOBBnIUW4Xr1OuGDvkDbllhoUm1y5y6EDnYqmD0T6NtqtTFzhG9Vkn4RJu_TCQuvEKfC5wzYHaqTgJuSj-LDIRqa6HRXGVuiEixwtHbygP778-Jafey_2IdID3RPFONDhoCcP-KOzUyduE7Z1NTe7dvERc75cjhtioKvVENg7DidzGrbbpXKz6xlYUXorT4UFGNpK4Ztbf3HySPYp4_fzJj2MOmMJynP8Pf3TVhgR-PcQRPRfCXXWlTyEzY_E0zFf9oZEeuhV9PUDrVYpK6GgO_-V0Jx2B0fFQtBaKIYCLAFvIReT_d4oU2tbwhtKLNJG3uEJuzrkjzd26zXnIqwLprTM7nDb_n7pihEw9LV5plu3)
</div>

### Sequence – ارسال فاکتور به سرویس ابری محک
<div align="Center"> 

![Sequence Modian](https://www.plantuml.com/plantuml/svg/TPBHwjCm5CRlynI7NEX_Q3lOPIzaeufs6ZUCQwzZ4romJMgJTWmHV0VVq2VnD0rqW_qlIiavl_ETxmlPEYzwFxGDUGcR5BZwEIXJA_ZtvoyUZ8J2Z5PZmLjWuYn-GAM-OQSViKX4xMqF9wTwqg6ChdKdZ0SQXqgjBXI4W_BPDhDIDJF37a9nLK3uFH7ye9s8v8rMnWUmUaH2tjX1mkvO10R_X4pM8Na3PGPvhuHNy6A97HFgSQgNf0mWomAGsxOLHjxq6IdPHF0CtYkZUYpkdJL7SMsia4yhmY690dj--0ouJbxZJCLdrRXrvwwcVkhcoTMo0sDLVEBHUmR70_yAQz7fzRXPwtdIBJ0o13z8eluleCuBFpYQKNxAytUSqzT0us0XiSm-V4pIDANmcqXr9rGjvZ_Px-266dSvU0LVL6kHATw69FDDyhEz0CKyFhoQvUxfhMp5RqybkpkHhJ8IN-L_)
</div>

### Sequence – ثبت خودکار سند حسابداری
<div align="Center"> 

![Sequence Document](https://www.plantuml.com/plantuml/svg/RP4_JiCm5CPtd-Af2qKeCB1rG3K9I47A52cxQpyLIubTxEV0o1su8IVXfKcKL7IA5F--Fv-zZwG2fQuLD_1u3pL-97GQuVVx1sGYd-c0YX2arZuviku8XTUfGqVYn4ghxKavWgO25M5JkjvRZOt5pyeRR3SNK5cleHf3pvzBH8x84dULAfxFL778lIFyeeqGN21xueGTrAh7AM9xAvGcs_C2FXASpuna9Z-lcfUy1j_zLp0evA9GhKxjyBl0WwK7TZ2MWDN1OXn1xhK3QSnsDeOxUFCfEDM-ZDpYpgpW6TbaFvJEtvKxOkGA1jVOu3rjcurBisRaE8sPfcAhf3N6oDdNQRw8FJh3R_u7)
</div>

### ER Diagram (بخش کلیدی)
<div align="Center"> 

![ER Diagram](https://www.plantuml.com/plantuml/svg/dPJFRjim3CRlVWeXns5vWQ98soLjuVqfFBJ5ph94T0GiSP2e04NTTv-ys1aTQsYnIo9HfFZZfo-vZAm39zTLu1dvMQrgloSqi58lbL8VQglEr6r2gyxFco-RJOwjr_bZpBfBheMGKo87z4_vOASPydxuUa07ET90YEJbHJU7Ynw8TNVbA7dEPnOCEjqDLv19BkCSIox-rlo0zXx27WsC1Ckar-fqbfh1lM-U0cKJo2R3XPFlIH_wIFX7Zzm4D30V2QEPpoanfu7VO9pIZgAZvwBYEuWcu2z6yk9f3dhle4M1COMt0Un9l8wVTAUzWG6d9PeXVwOKlEwkFOVdzs6N5BmoVrJPaYqflqHTKfPd5Q2YnHkSGugKwqwxsRxHuH-c_0fxwCRt4AqNNlrl3pwYbIJth3d5MGIyFV71HGvVXq3X6yIedw2epfQS8vkNjHtXbdRFZ1zl1EOjev_fr4OiqObsusIgxzThUb7YPpaxwlkZMQffCTL8mrLoervfg9HUgiHwgfUXCxKwFARQgErFxEngJjWl_sQgKPSfGGXNNOAtoNM_0G00)
</div>

### Component Diagram
<div align="Center"> 

![Component Diagram](https://www.plantuml.com/plantuml/svg/POuz2i9044RxFSLd6gju00j9t1WK5D9P3ycI1FTdsKpmP9x6opYn28BLWxTlFwQOc1BFpgeD3yOPq7FAGoBV6xN5-xM33Yu6RpoZ6gbFv5Ixckn60prmRsgKCMQWQU5lS0qjMLJ7vKtm_rVRC7Secykt42eb4yZpW-JOurH3XsHMAONOCtFKTfGTLHZVoVqV)
</div>

### Deployment Diagram
<div align="Center"> 

![Deployment Diagram](https://www.plantuml.com/plantuml/svg/LP11ImCn48Nl-HMFlQZ8hZSF7gJQU2XO4LVfGJrCTmTTccH2aXQA-D-Tj29uIkQzb_U5cUL2gMozCoUux60vEjbx3WLseez4tWGP6SrBveJ7EIum5nyfxD5psd5gy6M0roLzqWRTmzqpBETDaOYR6Dz1kPwQ6AdGch8stSj03lPtRch4tfflOmOdsn7D8XHEWSk_vXMl3y1fuBTmwglMvkFSJUdi05gk-bgZFBJjjPRY2aTOXV_f6bEZvp1Y2ZlHXcogLZtDgFV4EKhGlvxhrKjXBAoPwGDTqmy0)
</div>

### Activity Diagram
<div align="Center"> 

![Activity Diagram](https://www.plantuml.com/plantuml/svg/NP8zajD048LpdQ8pl0Mi0Z8Ji2ujWVa1iowA8fmTjUMkdP-XkyUKCkx03Ja9BTbejuYaKd_zdjwRkH5rh3M6vXcykeQDLpgHZd1BRc0NuS-ltz3bM08gmZQTCdbxYbHA0-muUnHfPescMNyLPCW5aope8NDytQpV9hKHAKPv0J-gIqfAQE-5ZH8ZDgM44G8bR0VEjRGzYSyrgSqw5tmDJX4qgmk6DtI0rSwD4PE2ZWNVN84UCS6gSt9iEyVzLGEmliE1PB8k5vPYn9vCAemD1a5ROFkWRNT4_z1kavX1cD1vVuy1lIxRYXobmTJJmUBktGc1Ba53zhOuJacgvfUUqKp0-Jd3L5QVVOquvzcFeXXXm8HibC2xN3cv05OJ4_xBjpSZq0mVtT4zm3UyXptoQJB3vEu3zalexoZpxrfHuOmRVO6xGEPwFObT3cKriPF1PhS5HYav2SBdz__BJVcF-IVSOSnFJ__sFFkG1v3gFOe09NXqj84HvtO_vQTAo9mPdiENYdM-6y2eF3xg7Ho5oZYjpoKl8alfEwQaI-ijC7gaOgsAvjBS65PZ-0i0)
</div>

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
