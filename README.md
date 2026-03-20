# Data Cleaning & Preprocessing Project

## Overview
هذا المشروع يهدف إلى تنظيف ومعالجة مجموعة بيانات (Dataset) تحتوي على أكثر من **10,000 سجل**، وتحويلها من بيانات خام مليئة بالأخطاء إلى بيانات دقيقة جاهزة للتحليل بنسبة **98%**.

---

## 1. Data Audit (مرحلة الاستكشاف)
تم فحص البيانات ورصد المشكلات التالية:
* **Missing Values:** وجود **3,265** خلية فارغة.
* **Invalid Data:** رصد قيم نصية خاطئة مثل (`Unknown`, `Error`) تزيد عن **400** تكرار في أغلب الأعمدة.
* **Inconsistent Types:** الأعمدة كانت بصيغة نصوص (Objects) مما يعيق العمليات الحسابية.

---

## 2. Preprocessing Steps (خطوات المعالجة)

### 🔹 Step 1: Type Conversion
تم تحويل أنواع البيانات إلى الصيغ الصحيحة لضمان كفاءة الذاكرة ودقة الحسابات:
- `Transaction Date` ➡️ **Datetime**
- `Quantity` ➡️ **Integer**
- `Price per Unit` & `Total Value` ➡️ **Float**

### 🔹 Step 2: Initial Imputation (المعالجة المبدئية)
- تم استبدال القيم التالفة بـ `0` في الأعمدة الرقمية كـ (Placeholder).
- تم توحيد القيم المفقودة في الأعمدة الوصفية (Location, Payment Method) بكلمة `Unknown`.

### 🔹 Step 3: Logic-Based Recovery (التنبؤ المنطقي)
تم استخدام علاقات البيانات لتعويض المفقود بدلاً من حذفه:
* **Item ↔ Price Mapping:** بناء قاموس مرجعي للمنتجات وأسعارها (بعد التأكد أن الموقع لا يؤثر على السعر).
* **Cross-Filling:** تنبؤ اسم المنتج المفقود من سعره، والعكس.
* **Mathematical Recovery:** - حساب الكمية: `Quantity = Total Value / Unit Price`
  - حساب الإجمالي: `Total Spent = Quantity * Unit Price`

---

## 3. Final Results (النتائج النهائية)

| Metric | Before Cleaning | After Cleaning |
| :--- | :--- | :--- |
| **Data Accuracy** | ~65% | **98%** |
| **Clean Records** | Mixed / Corrupted | **9,930 Records** |
| **Dropped Rows** | 0 | **70 Rows (Only 0.7%)** |

> **Conclusion:** تم الحفاظ على هيكل البيانات الأساسي وتقليل الفاقد لأدنى درجة ممكنة مع ضمان اتساق العمليات الحسابية بنسبة 100%.

---

## 💻 Tech Stack
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
