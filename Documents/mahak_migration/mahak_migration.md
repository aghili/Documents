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
![Class Diagram]()

### Sequence – ارسال فاکتور به مودیان
![Sequence Modian](https://www.plantuml.com/plantuml/png/TPF1RjD048Rl-nGZdsn1qtiFgAMDK12XaPmYhYjdXImbTkGu9H7YK4GJ3Zm55wULI8XAGRtqESRbPVXdrpHEHI-RtUmt_ypyizuVvJhBnuE-qb6UPdHtmGMlUS5hDSH57CL3dUJajPBJD8xCczYyzqYFI3QF4ksqP_eEQ_yN2arsYX-Bo7uRGdYiarQIctUPpkCqgUFkSZlWeDEYyfnl-1BhYdoiHJddzQxTVFxp5HTVU1rO0S3RqNm5IC1PEOSCo1KYSBHuLq-KshX2EyzixxH7VCqhaQNoZ0iGDWSzWOMIykw2F1jq9IKGBnwAAoiZScs8XIRfTLFNt64w6EYarsXEJ3JEZHye80351g0lJ6BWYt5mHq_xgUxviNCsK9RQ-QVxCZn-lVks_Ohuc_I8YkULcWklKbTpEHXDayWVEib0EGImc0QoSnnsQRVAD28VXXGaVQFbMQ00WHN7mDPxlnPd-9A_on-yK4BitAkMjrpWOad-IUi8_W7-nJSoj4goNkm7yiPnpziZhz5eU4_9m_lDnoFv8pmvF6o6eKSVgy8tBhXprIJg_i5BwAyn4bvXPaVFdSMRsPOpSGlCp_eKxG3Bi_AJXp9Hh1kXXDKUI3qOlTbfdzz7IbjAwNvElEJVNBW2DYaKqSFYcvF83EKp81zfLbLW0FBHcXqYNjxAMLwsp9uoasTJXNchVIpuwly2)

### Sequence – ثبت خودکار سند حسابداری
![Sequence Document](//www.plantuml.com/plantuml/png/RPBD2fj058NtFiN5bI4qtNTHyfCMKd3JWFkf3gcGp8YEIRTTDCaYxv7KjeZOXvbfNgR7c075B6JkFVUxFnoSPegbAjzjdGHl7CO94uhSbTZBEEH1p0--ZFZM9PPHuB-4rZpTutaWa9gqpyt2KEP2nMBJHQ4EqQKCynqNocU2RNWJTLjGVJ4zIPPV5b8e_asrrDnn0f_UlBVNq3jQipr_dkl5xJjoR1aaZdcIYvGpnUqT7rEv6_G17lQP7_gFlkfQtyo9z4sNvlJl9uJgBP9Q5_fgZgr07iWQqOtCTrsPi_whB-X7y1jVURyyKgY5hku8ppIPJ3fhiNSfxLx13sIlfJ5zadagsFQ3K6dCCyToJSiSz2oAF4kFNbK_Cx7XNdyAm7bdg_LpyRLXCwypf-U8tREAUgV3pY7GY1O8VDIUfjEuIw7I0AsDiBK2wCB3AvJ2d973ArsReov9_m9G45miNMVAHOH__3y0)

### ER Diagram (بخش کلیدی)
![ER Diagram](//www.plantuml.com/plantuml/png/dPHTJjmm4CVVSmfh7wlk1H1QeBk0qXQKgd00hpsY8yMUoXuZ8SBTwpJ9Thou0l6IsFFX-StVavn7re6JwnlmZFoaLgr_93ImKi-DKfzQgqxKTKAhJa-xRvjDjgtN-J57tIQtXv138WVq3zcnqmnvFxxkq46sT10YUNdGrNJG7R7kBnmbpzbdmQ3J_NW4cUGopY7bx5_E3LdKVgx-Ek2bEUwZPN3lwwL2s0MooN35yoFfgOu4l_V8NK03PJiOJTcZn5oQVODn2Ji8ZfwhQkyWce2_6ScBQvcqti4U9SPitWQmH_OsVj6zzWP6d3rHWVoLKl2wl_GSdjw9NL7mmlnLPKksflnhr0fbjLS1AagymJc6IBbkjIlsdGx_6SZly0ZzV1-YT36d7vw_UxIIuYThJh6mWBT7Ct2MpPSXKBY16FK3L9NPadDayxArCrmvwZFZvok1USte2uts4IjqijpScHg6zPgUbVWa2zSm70QbMHPBZXosHcxK2usPSeuQiLxofUb4hQQBL1kr_OMzNPM4G_bxQMPD5gSGhJa7RvFh_m00)

### Component Diagram
![Component Diagram]()

### Deployment Diagram
![Deployment Diagram](./puml/deployment_diagram.puml)

### Activity Diagram
![Activity Diagram](https://www.plantuml.com/plantuml/png/RL9DxfDm4Dt_JZ7kR8nXtswwSEC1F40JgJRfXw4OunB21mlku1AA5YGqDcnwZXcuZ6y0e_Z_9mtjpFlecnVMPtVZk9yFU_F2_MWVRDfyERy-EPlZ1ziCa5bAmXdNN55tqI-9Y3Fn9S0p9F4umxu0gLwP9PYjX402ue9ByVfKF8kluXCtN4lIfzo01ywLCwnoYOb_O6n98eavwzC-NPdTbbvYJh26JwCwWDyMX9370VAvwjE58LhoTywv87beEfYMEam42zaqV67i_TbM8JTgPNLHTx7q3cv0k8z66M2anY8dla66D7oVEHlx-7wtnQ4_kGHOIpohWC3J1w12RQPp5PG0GqLSWbUDiT29HBgx3YboYB7zS_yGl1cxr9eaX1BE6bF_j5NeRoVW119FXyoLm-zGTV_PW3mqZPLuuZzd1Zl888RYHk_UlY59yE5VtEgHO8pDZdKyLQ2qEsVqYlvfZFEnMt9ir_aAoLZgt6WgkeiGz34hsH9FhLTuGK-Vp1f4lB-_0G00)

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
