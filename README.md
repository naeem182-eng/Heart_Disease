#  Heart Disease Prediction - Super AI Engineer Season 6

โปรเจกต์ทำนายโอกาสการเป็นโรคหัวใจ (History of Heart Disease or Attack) โดยใช้ข้อมูลพฤติกรรมสุขภาพและปัจจัยพื้นฐานจากชุดข้อมูลการสำรวจสุขภาพ พัฒนาขึ้นเพื่อใช้ในการแข่งขัน **Super AI Engineer Season 6**.

##  Overview
โมเดลนี้ถูกออกแบบมาเพื่อช่วยคัดกรองผู้ที่มีความเสี่ยงเป็นโรคหัวใจ โดยให้ความสำคัญกับการลด **False Negative** (การตรวจไม่พบในคนที่เป็นโรคจริง) ซึ่งมีความสำคัญอย่างยิ่งในทางการแพทย์

##  Data Cleansing & Features
เพื่อให้โมเดลมีความแม่นยำสูง เราได้ทำ Preprocessing ดังนี้:
* **Missing Value Handling:** เติมค่าว่างด้วยฐานนิยม (Mode) สำหรับข้อมูลกลุ่ม และค่ากลาง (Median) สำหรับข้อมูลตัวเลข
* **Feature Encoding:** * แปลงค่า Binary (Yes/No, Male/Female) เป็น 1/0
    * จัดระดับข้อมูล (Ordinal Mapping) สำหรับระดับสุขภาพ (General Health) และการศึกษา (Education Level)
* **Outlier Management:** ตรวจสอบและจัดการค่า BMI ที่ผิดปกติด้วย `pd.to_numeric`

##  Machine Learning Model
* **Algorithm:** LightGBM Classifier
* **Validation Strategy:** Stratified K-Fold Cross-Validation (5 Folds) เพื่อรับมือกับข้อมูลที่อาจมีความไม่สมดุล (Imbalanced Data)
* **Optimization:** ปรับจูน `class_weight='balanced'` เพื่อให้โมเดลให้ความสำคัญกับกลุ่มที่เป็นโรคหัวใจมากขึ้น

##  Evaluation & Threshold Tuning
เนื่องจาก Metric หลักคือความแม่นยำในการคัดกรอง เราจึงใช้เทคนิค **Threshold Optimization** เพื่อหาค่าจุดตัดที่เหมาะสมที่สุดในการทำนายผล โดยพิจารณาจาก:
* **F2-Score:** เพื่อเน้นค่า Recall ให้มากกว่า Precision (เน้นการเก็บตกผู้ป่วยให้ได้มากที่สุด)
* **Confusion Matrix:** วิเคราะห์ความสัมพันธ์ระหว่างการทำนายจริงและการทำนายผิด

##  How to use
1.  Clone this repository.
2.  Install dependencies: `pip install lightgbm pandas scikit-learn`
3.  Run the notebook in Google Colab or Local Jupyter.

---
**Author:** Isares 
**Project Part of:** Super AI Engineer Season 6 Training Phase
