---
title: "OCR Text Extraction From Student Card"
excerpt: "Developed an OCR system for Dawnvale Academy of Medicine student cards. It detects card corners, adjusts orientation if needed, and extracts name, member ID, address, phone number, district. Utilizes similarity measures against a district master dataset for accuracy. <br/>
    <img src='/images/ocr_streamlit.png'>"
collection: portfolio
---

**Project Background & Description**
 
<span style="font-size: 12px;">[Click here to visit github repo](https://github.com/deviyantiam/student_card_ocr)</span>

Our Student Card Scanner is a smart tool designed for a fictitious educational institution, Dawnvale Academy of Medicine (dummy data  was made using Canva)

Key Features:
1. Corner Detection:
the scanner spots the corners of the card and adjust orientation if needed
2. OCR:
it scans ID cards and converts into text
3. Data Extraction:
it retrieves important details from scanned ID cards such as names, ID numbers, addresses, and phone numbers. Including double-check district info we extract by comparing it to master data and return the closest match from the list

Plus, we've wrapped it all in a API and a Streamlit interface for demo

## Corner Detection

1. **Data Preparation**
   - Gather student card images, including rotated variations
   
2. **Labeling with LabelIMG**
   - Annotate corner points on images using LabelIMG
   ![labelimg](/images/ocr_detect.png)

3. **Convert to COCO Format**
   - Convert annotated dataset from Pascal VOC to COCO format for Detectron2 compatibility

4. **Training**
   - Train Detectron2 with the converted dataset (10 images).
   ![traning](/images/detectron2_test_eval.png)

5. **Predict**
    - predict corner detection on test data
![test data](/images/detectron_test_result.png)

To note: Our Detectron2 model for student card corner detection was trained one time due to resource constraints (CPU only). Although initial performance may be suboptimal, we improved accuracy by addressing duplicated output in subsequent OCR tasks.

6. **Duplication Correction**
    - Address duplicated output in OCR tasks to enhance model accuracy
![cleaned test data](/images/detectron_test_result_cleaned.png)
7. **Reorientation or Crop if Needed:**
   - Utilize corner detection results to reorient or crop images as necessary for further processing
![reorientation](/images/detectron_result_2.png)
![crop](/images/detectron_result.png)


## OCR
1. **Prepare Data**
- Utilize the EasyOCR available model, to convert images to text and generate cropped images. Relabel if needed
![relabel](/images/ocr_relabel.png)
2. **Train EasyOCR**
- I trained two models. The first model was trained without using a pre-trained model and was limited to 1000 iterations due to resource constraints (CPU only). However, its performance did not meet my expectations. Subsequently, I trained a second model using a pre-trained model, also limited to 1000 iterations. This resulted in a notable improvement in performance, as discussed in next subheader evaluation.

wo pretrained model
![wo pretrained model](/images/ocr_training.png)

w pretrained model
![w pretrained model](/images/ocr_pretraining.png)


## Data Extraction
I made a function that retrieves important information like names, ID numbers, addresses, and phone numbers from scanned ID cards. It double-checks district information by comparing it to master data, finding the closest match from the list, and obtaining the district code based on the selected district name from the master data.

result of test data with v1 model
![result v1](/images/ocr_v1_eg.png)

## Evaluation
I use 3 metrics:

- CER (Character Error Rate): It measures the percentage of incorrectly recognized characters compared to the total number of characters in the ground truth text. A lower CER indicates better accuracy in recognizing individual characters.
- WER (Word Error Rate): It calculates the percentage of incorrectly recognized words compared to the total number of words in the ground truth text. WER takes into account both substitution errors (wrong words) and insertion/deletion errors (missing or extra words). A lower WER signifies better accuracy in recognizing entire words.
- Accuracy in the context of this project is achieved when the Word Error Rate (WER) equals zero, meaning there are no errors in recognizing words compared to the ground truth.

Performance:
- V1 on test data (normal orientation):

![v1](/images/ocr_result_v1.png)
- V2 on test data (normal orientation):

![v2](/images/ocr_result_v2.png)
- V2 on rotated test data:

![v2 - rotated](/images/ocr_metrics_rotated.png)

model v2 was chosen

##  API & Streamlit
![API](/images/ocr_result_api.png)
![Streamlit](/images/ocr_streamlit.png)
![Streamlit 2](/images/ocr_streamlit2.png)

category: 
<button onclick="window.location.href='/ocr';">OCR</button>
