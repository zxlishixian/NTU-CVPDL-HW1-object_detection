# HW1 — OBJECT DETECTION作業 README

> 這份 README 為 HW1 - OBJECT DETECTION 作業的說明文件，利用yolo架構實現對照片中豬的識別，並輸出作業要求的提交格式。從零安裝環境、準備資料夾、執行**訓練**與**推理/產出提交檔**。核心程式在 `HW1_3.ipynb`
---




## 專案結構

請確保資料夾結構長這樣（檔名可不同，但層級需一致, 其中 output 和 runs 文件夾會由程式自動生成，可以不需要預先創建）

```
.
├─ HW1_3.ipynb
├─ data/
│  ├─ train/
│  │  ├─ img/                 # 訓練影像 ( 00000001,00000002...  jpg/png...)
│  │  └─ gt.txt               # 訓練標註     
│  └─ test/
│     └─ img/                 # 測試影像（無標註）
├─ (output/ )                    # 由 notebook 產生（提交 csv、統計等）
└─ (runs/   )                    # Ultralytics 的輸出（訓練/推理結果）
```
---


## 環境安裝

### 建立 Conda 環境

```bash
conda create -n hw1-od python=3.10 -y
conda activate hw1-od
python -m pip install --upgrade pip
```

### 安裝 PyTorch

擇一安裝（依你的設備）：

- **CPU 版：**
```bash
pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu
```

- **CUDA 12.1 版（若顯卡/驅動支援）：**
```bash
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121
```

> 其他 CUDA 版本請改用相對應 index（如 `cu118`）。

### 安裝其餘套件

```bash
pip install ultralytics pandas numpy pillow ipython opencv-python jupyterlab
```

## 運行cell1 將data中的數據集轉換成yolo架構可接受的格式
這個cell的程式會將標準數據集data文件夾中的文件轉化成yolo架構要求的輸出，正確運行後會在與data同層級目錄下產生一個名為data_yolo的文件夾
```


-- data_yolo/
    |
    ├─dataset.yaml
    |
    ├─ images/
    │  ├─ train/                 
    │  ├─ test/       
    |  └─ val/
    |            
    │  
    └─ label/
       ├─ train/       
       └─ val/                
    
```

建議檢查dataset.yaml中的配置是否正確再進行下一步
---



## 運行cell2 利用yolo架構開始訓練

這個cell的程式運行後正式開始利用data_yolo中的數據集開始訓練，會在與ipynb文件同層目錄下產生run/detect文件夾後,在裡面產生train，train1，train2...文件夾（每訓練一個新模型就會產生一個新的train文件夾），train文件夾裡面有pt後綴即為訓練的模型參數配置，還有一些其他記錄訓練過程的文件
---


## 運行cell3 對驗證集開始測試，並在runs/detect下產生val文件夾，記錄驗證結果的指標
---

## 運行cell4 產生對test預測的結果

請將這四行的參數改為你實際的路徑：

MODEL_PATH     = r"C:\Users\11958\Desktop\vscode-c\c\cv\hw1\runs\detect\train22\weights\last.pt"    # 你的权重

TEST_IMG_DIR   = r"C:\Users\11958\Desktop\vscode-c\c\cv\hw1\data\test\img"      # 测试图目录

PROJECT_DIR    = r"C:\Users\11958\Desktop\vscode-c\c\cv\hw1\runs\detect"        # Ultralytics project 路径

RUN_NAME       = r"pred_test/result_picture"                                     # 会拼成 runs/detect/pred_test/result_picture

SUB_CSV_PATH   = r"C:\Users\11958\Desktop\vscode-c\c\cv\hw1\runs\detect\pred_test\sub\submission.csv"

運行後會在runs/detect目錄下產生一個pred_test文件夾：
裡面的result_picture文件夾用於存放對test中的圖片預測的結果圖片，給每一個被檢測的物體標記框與置信度；
sub文件夾用於存放產生的submission文件，如果重複運行每一次產生的文件會覆蓋重名submission文件，所以要記得每一次運行都要更改
SUB_CSV_PATH   = r"C:\Users\11958\Desktop\vscode-c\c\cv\hw1\runs\detect\pred_test\sub\submission.csv"和out_csv = Path(r"runs/detect/pred_test/sub") / "submission_17.csv"的路徑
---

## 運行cell5 將讀取pred_test/result_picture的前五張圖片，便於直接判斷該次預測表現是否良好
---
