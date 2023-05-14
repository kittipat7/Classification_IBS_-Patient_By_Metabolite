# Classification_IBS_Patient_By_Metabolite
## โรคลำไส้แปรปรวน (irritable bowel syndrome หรือ IBS)  
- โรคลำไส้แปรปรวน (irritable bowel syndrome หรือ IBS)  เป็นโรคของลำไส้ที่ทำงานผิดปกติไป ทำให้เกิดการปวดท้องร่วมกับมีอาการท้องเสียหรือท้องผูก หรือท้องเสียสลับกับท้องผูก โดยที่ตรวจไม่พบพยาธิสภาพที่ลำไส้ เช่น ส่องกล้องตรวจลำไส้จะไม่มีอาการอักเสบ ไม่แผลไม่มีเนื้องอกหรือมะเร็ง รวมทั้งไม่มีโรคของอวัยวะอื่น ๆ ที่จะมีผลให้การทำงานของลำไส้ผิดปกติ เช่นโรคต่อมไทรอยด์เป็นพิษ หรือโรคเบาหวานเป็นต้น โรคลำไส้ทำงานแปรปรวนจะเป็นโรคเรื้อรังอาจเป็นปี ๆ หรืออาจเป็นตลอดชีวิต เป็นโรคที่ไม่ทำให้สุขภาพเสื่อมโทรม แม้จะเป็นมาหลาย ๆ ปี และไม่ทำให้เกิดอันตรายถึงแก่ชีวิต แต่เป็นโรคที่สร้างความรำคาญ และความทุกข์ทรมานให้ผู้ป่วยอย่างมากได้ 
## การตรวจวินิจฉัยโรคลำไส้แปรปรวน
- จากพยาธิสรีรวิทยาและกลไกการเกิดโรคที่ซับซ้อนบอกให้ทราบว่า โรคลำไส้แปรปรวน IBS เป็นความผิดปกติในระดับเซลล์ มองไม่เห็นด้วยตาเปล่าและไม่สามารถจับต้องได้ การตรวจทางห้องปฏิบัติการ หรือภาพเอกซเรย์ช่องท้อง รวมถึงการส่องกล้องตรวจลำไส้ใหญ่จะให้ผลเป็นปกติในขณะเดียวกันอาการของโรคลำไส้แปรปรวน IBS จะมีความคล้ายคลึงกับ โรคลำไส้ชนิดอื่น ๆ ด้วย เช่น โรคลำไส้อักเสบจากการติดเชื้อโรคต่าง ๆ (เช่น เชื้อแบคทีเรีย พยาธิ โปรโตซัว เอชไอวี วัณโรคลงลำไส้), ลำไส้เป็นแผล, โรคลำไส้อักเสบเรื้อรัง IBD  และนอกจากนั้นในทางพยาธิสรีรวิทยา พบว่าจุลินทรีย์ในลำไส้และ metabolites สามารถตรวจและแยกประเภทโรคลำไส้แปรปรวนได้ 
## วัตถุประสงค์
- เพื่อสร้างตัวแบบ Machine Learning จำแนกประเภท ระหว่าง ผู้เป็นโรคลำไส้แปรปรวน และผู้ที่ไม่เป็น จากสาร Metabolite
- หาว่าสาร Metabolite ชนิดใดที่ส่งผลต่อการเป็นโรคลำไส้แปรปรวน
## Data
- ในการศึกษานี้ใช้สาร Metabolite ที่สกัดจากอุจจาระ โดยตัวข้อมูลประกอบด้วย metabolite 601 ชนิด และ column ที่ระบุว่าเป็นผู้ป่วยหรือ กลุ่ม healthy controls รวม 602 columns
และ มีผู้ป่วยโรคลำไส้แปรปรวน 229 คน กลุ่ม healthy controls 139 คน โดย data set ชุดนี้ไม่มี Missing values
## วิธีที่ใช้
- โดยวิธีที่ใช้นั้นจะมีการทำ Feature selection ก่อนเข้า Classification Model และวัดผลด้วย AUC Score
### Feature Selection
- ในส่วนของการทำ Feature selection จะใช้ Recursive Feature Elimination with Cross-Validation(RFECV) เป็นการวนลูปเลือกฟีเจอร์ หรือกลุ่มของฟีเจอร์ แล้วทำการทดสอบการสร้างโมเด เพื่อหาว่า ฟีเจอร์ชุดใด ทำให้สามารถสร้างโมเดลที่มีประสิทธิภาพสูงสุดได้ จากนั้น จึงเลือกฟีเจอร์นั้นๆ เพื่อใช้งานต่อไป โดยหลักการทำงานในการเลือกฟีเจอร์ ก็คือ เริ่มต้นด้วยการใช้ฟีเจอร์ทั้งหมดก่อน และทำการ ตัดฟีเจอร์ที่มีความเกี่ยวข้องน้อยที่สุดออกไป เพื่อทำให้ขนาดของฟีเจอร์ลดลง จนกว่าจะได้มาซึ่งชุดของฟีเจอร์ที่เล็กที่สุดและ เนื่องจากข้อมูลที่ใช้มีสาร metabolite 601 ชนิด หรือ ตัวแปรอิสระ (X) เป็นNumeric และตัวแปรตาม (y) เป็น category จึงเลือกใช้ Linear discriminant analysis (LDA) เป็นตัว estimator และ วัด Coeficient ของ ตัวแปรอิสระ (X) แต่ละตัวที่ส่งผลต่อตัวแปรตาม (y)
- และเนื่องจาก Recursive Feature Elimination with Cross-Validation(RFECV) เป็นวิธีการ เป็นการคัดเลือกฟีเจอร์ด้วยการสร้างโมเดล (classification model) ขึ้นมาจากเซตของฟีเจอร์ที่กำหนดไว้และวัดประสิทธิภาพการทำงานของโมเดล และเลือกเซตของฟีเจอร์ที่ทำให้โมเดลมีประสิทธิภาพมากที่สุดมาใช้งาน ซึ่งอาจจะไม่สามารถอธิบายได้ว่า Feature แต่ละตัวส่งผล ตัวแปรตาม (y) จริงหรือไม่ จึงเลือกใช้ ANOVA and the Bonferroni Correction ทำ Feature selection โดยทดสอบ  Feature แต่ละตัวเทียบกับ Recursive Feature Elimination with Cross-Validation(RFECV)
- One-Way ANOVA and the Bonferroni Correction เนื่องจากต้องทำการเปรียบเทียบกันหลายครั้งในที่นี้มี สาร metabolite 601 ชนิด ซึ่งเสี่ยงกับการทำให้เกิด False Positive ได้ จึงป้องกันโดยใช้ Bonferroni ในการปรับค่า alpha รายคู่ 
- ทดสอบค่าเฉลี่ยของ metabolite ที่ถูกเลือกระหว่าง ผู้ป่วย กับ กลุ่ม healthy controls ว่าต่างกันจริงหรือไม่ ด้วย t-test
### Classification Model
- Logistic Regression
- K- Nearest Neighbor (KNN)
- Support Vector Machines (SVM)
## ผลลัพธ์
### Feature Selection with Recursive Feature Elimination with Cross-Validation(RFECV) 
ผลลัพธ์จาก Recursive Feature Elimination with Cross-Validation(RFECV) ที่ใช้ Linear discriminant analysis (LDA) เป็นตัว estimator สามารถลดจำนวน metabolite จาก 601 ชนิดเหลือเพียง 10 ชนิด
ได้แก่ 2-hydroxyglutarate, 2-isopropylmalate, gamma-glutamylleucine, glycine, glycylvaline, lactosyl-N-nervonoyl-sphingosine (d18:1/24:1)*, lactosyl-N-palmitoyl-sphingosine (d18:1/16:0), oleoyl ethanolamide, serine, xylose
#### Logistic Regression
ใช้ Feature ที่ถูกเลือกจาก RFECV กับ Logistic Regression

![image](https://github.com/kittipat7/Classification_IBS_Patient_By_Metabolite/assets/97491541/d00512b8-b589-4357-8809-c0169e3f3be8)

#### K- Nearest Neighbor (KNN)
ใช้ Feature ที่ถูกเลือกจาก RFECV กับ K- Nearest Neighbor (KNN)

![image](https://github.com/kittipat7/Classification_IBS_Patient_By_Metabolite/assets/97491541/4c133447-e9fe-41ad-8cd9-19e1ea12d9d5)

#### Support Vector Machines (SVM)
ใช้ Feature ที่ถูกเลือกจาก RFECV กับ Support Vector Machines (SVM)

![image](https://github.com/kittipat7/Classification_IBS_Patient_By_Metabolite/assets/97491541/ac51e2a8-afc9-4afe-b217-9ff36ff7a9d7)

### One-Way ANOVA and the Bonferroni Correction
ผลลัพธ์จาก One-Way ANOVA and the Bonferroni Correction สามารถลดจำนวน metabolite จาก 601 ชนิดเหลือเพียง 22 ชนิด ได้แก่ 1-methyladenine, 2,4-dihydroxyhydrocinnamate, 2-keto-3-deoxy-gluconate, 3-phenylpropionate (hydrocinnamate), 5alpha-androstan-3alpha, 17alpha-diol disulfate, acesulfame,allantoin, arabinose,carboxyethyl-GABA, ferulate,gamma-glutamylleucine, leucylglycine,
 N-acetyl-1-methylhistidine*, N-acetylmuramate, naringenin, N-delta-acetylornithine, N-palmitoyl-sphinganine (d18:0/16:0), ribulose/xylulose, salicylate, serotonin, valine betaine, xylose
#### Logistic Regression
ใช้ Feature ที่ถูกเลือกจาก One-Way ANOVA and the Bonferroni Correction กับ Logistic Regression

![image](https://github.com/kittipat7/Classification_IBS_Patient_By_Metabolite/assets/97491541/9de6ac05-f36a-4d5b-a9ac-22ff1767ebea)

#### K- Nearest Neighbor (KNN)
ใช้ Feature ที่ถูกเลือกจาก One-Way ANOVA and the Bonferroni Correction กับ K- Nearest Neighbor (KNN)

![image](https://github.com/kittipat7/Classification_IBS_Patient_By_Metabolite/assets/97491541/f4352b0b-5eea-4642-9737-04c626da12b0)

#### Support Vector Machines (SVM)
ใช้ Feature ที่ถูกเลือกจาก One-Way ANOVA and the Bonferroni Correction กับ Support Vector Machines (SVM)

![image](https://github.com/kittipat7/Classification_IBS_Patient_By_Metabolite/assets/97491541/c62ba09c-efbe-4e4d-8e5e-c7389b63a8d6)

### สรุปผล
- Feature Selection with Recursive Feature Elimination with Cross-Validation(RFECV) มีประสิทธืภาพในการลดจำนวน Feature ได้ดีกว่า One-Way ANOVA and the Bonferroni Correction แต่เมื่อนำ Feature ที่ถูกเลือกไปใช้กับ Classification Model โดยผลลัพธ์ที่ดีสุดคือ Logistic Regression AUC Score ที่ 0.8651009316770185 ซึ่งต่ำกว่า การใช้ Feature ที่เลือกโดย One-Way ANOVA and the Bonferroni Correction ที่ถูกเลือกไปใช้กับ Classification Model โดยผลลัพธ์ที่ดีสุดคือ K- Nearest Neighbor (KNN) AUC Score ที่ 0.8879076086956522
## Reference
Lo Presti, Alessandra et al. (2023) Phylogenetic analysis of Prevotella copri from fecal and 	mucosal microbiota of IBS and IBD patients. Therapeutic advances in gastroenterology 	,16. 1-10.

Canavan, C., West, J., & Card, T. (2014). The epidemiology of irritable bowel syndrome. Clinical 	epidemiology, 6, 71–80.

Hussain et al. (2019). Classifying Cancer Patients Based on DNA Sequences Using Machine 	Learning. Journal of Medical Imaging and Health Informatics, 9. 436-443.

Jacobs, J.P et al. (2023). Multi-omics profiles of the intestinal microbiome in irritable bowel 	syndrome and its bowel habit subtypes. Microbiome, 11, 5.

Meesad, P., Wichian, S. N., Herwig, U., & Saengsiri, P. (2016). Classication Models Based-on 	Incremental Learning Algorithm and Feature Selection on Gene Expression Data. ECTI 	Transactions on Computer and Information Technology (ECTI-CIT), 6(1), 40–47.

Xiao, L., Liu, Q., Luo, M., & Xiong, L. (2021). Gut Microbiota-Derived Metabolites in Irritable 	Bowel 	Syndrome. Frontiers in cellular and infection microbiology, 11, 729346. 

อัจจิมา มณฑาพันธุ์. (2562). การเปรียบเทียบวิธีการคัดเลือกคุณลักษณะที่สำคัญในการปรับปรุงการพยากรณ์	มะเร็งเต้านม. Royal Thai Air Force Medical Gazette, 65(2), 49-55.

นพ.สุริยา กีรติชนานนท์. (2561).  โรคลำไส้แปรปรวน: อาการ หลักการวินิจฉัย และแนวทางการรักษา. ค้นเมื่อ 	24  กุมภาพันธ์ 2023 จาก 	https://bangkokhatyai.com/uploaded/content/link_130916101751392.pdf

