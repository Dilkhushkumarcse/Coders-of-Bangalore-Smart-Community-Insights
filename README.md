

---

# 🚀 Coders of Bangalore

**A complete data extraction and analytics project to identify the most active, influential, and diverse coders in Bangalore’s tech community.**

---

##  **Project Overview**

Coders of Bangalore is a data-driven project built to analyze community engagement by extracting details such as:

* Number of posts
* Followers
* Following
* Categories
* Bio and Profile Type

Using a custom parsing algorithm, it reads raw scraped text, converts it into structured JSON, and computes insights like:
- User with the maximum posts
- User with the maximum followers
- User with the maximum following
- Total number of categories

---
##  **Primary Objectives**

* Convert unstructured text into structured JSON
* Automatically identify top contributors
* Analyze user categories
* Build foundational analytics for Bangalore’s coder ecosystem

---

##  **Key Features**

###  **1. Text Parsing & Cleaning**

Your code splits raw text into blocks (chunks) and extracts:

* Username
* Number of posts
* Followers
* Following
* Name
* Page Type
* Bio

### **2. JSON Dataset Creation**

All parsed chunks are exported to `data.json` in a clean, structured format.

### **3. Insights & Rankings**

The script computes:

*  **Top poster**
*  **Top influencer (followers)**
*  **Most connected user (following)**
*  **Total number of categories present**

###  **4. Robust Number Conversion**

Handles conversions like:

* `12K` → `12000`
* `1.4M` → `1400000`

### **5. Modular Processing**

The `parse_chunk()` function is reusable and cleanly handles each section.

---

##  **How the Code Works (Step-by-Step)**

### **1️⃣ Splitting Data**

```python
chunks = data.split("\n\n")
chunks = [c for c in chunks if len(c) > 3]
```

* Splits raw text into user blocks
* Filters out empty chunks

---

### **2️⃣ Parsing Each Chunk**

The `parse_chunk()` function extracts details line by line:

```python
username = sep_chunk[0]
no_of_posts = int(sep_chunk[1].split(" post")[0].replace(",", ""))
```

### Followers + Following handle **K/M conversions**:

```python
no_of_followers = float(...)
if "K" in sep_chunk[2]: no_of_followers *= 1000
if "M" in sep_chunk[2]: no_of_followers *= 1000000
```

### Category & Bio handling:

```python
type_of_page = sep_chunk[5] if len(sep_chunk) > 5 else "Unknown"
bio = "\n".join(sep_chunk[6:])
```

---

### **3️⃣ Saving to JSON**

```python
with open("data.json", "w") as f:
    f.write(json.dumps(all_chunks, indent=4))
```

---

### **4️⃣ Finding Top Users**

#### Max Posts:

```python
for chunk in all_chunks:
    if max < chunk['no_of_posts']:
        chunk_with_max_post = chunk
```

#### Max Followers:

```python
for chunk in all_chunks:
    if max < chunk['no_of_followers']:
        chunk_with_max_followers = chunk
```

#### Max Following:

```python
for chunk in all_chunks:
    if max < chunk['no_of_following']:
        chunk_with_max_following = chunk
```

---

### **5️⃣ Counting Categories**

```python
categories = set()
for chunk in all_chunks:
    categories.add(chunk['type_of_page'])
```

---

## **Folder Structure**

```
Coders-of-Bangalore/
│
├── data.json               # Final structured dataset
├── final_data.txt            # Original scraped data
├── coders-of-bangalore.ipynb   # Python code for parsing + analytics
├── README.md               # Documentation
```

---

##  **Installation & Usage**

### **1️⃣ Clone the Repository**

```bash
git clone https://github.com/yourusername/Coders-of-Bangalore.git
cd Coders-of-Bangalore
```

### **2️⃣ Run the Script**

```bash
python script.py
```

### **3️⃣ Output Files**

* `data.json` → full parsed dataset
* Terminal → prints insights
* Can be extended to produce graphs

---

## 👨‍💻 **Developed By:**

**Dilkhush Kumar**
*Computer Science & Engineering | Data Science Enthusiast*

---
