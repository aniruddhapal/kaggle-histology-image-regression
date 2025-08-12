# End-to-End Histology Image Regression & Pipeline Optimization

This repository contains the code and documentation for my project on the Elucidata Global AI Hackathon '25 Kaggle competition. The primary focus is a deep dive into building, debugging, and optimizing a complete PyTorch pipeline for a complex multi-target regression task on histology images.

**The most significant achievement of this project was improving the initial competition score by 28.7% through rigorous post-competition analysis and code refactoring.**

**[View the Polished Kaggle Notebook](https://www.kaggle.com/your-username/your-notebook-url)** | **[Read the Full Story on my Blog](https://your-blog-url.com/your-article)** *(<-- Optional: Link to your blog post when ready)*

---

## 🚀 Project Outcome: A 28.7% Improvement

| Metric                      | Score     |
| --------------------------- | --------- |
| **Initial Score (at Deadline)** | `0.19677` |
| **Final Score (Post-Debugging)**  | `0.25311` |
| **Relative Improvement**        | **`28.7%`** |

This project serves as a case study in the importance of data integrity and systematic debugging. The final, high-performing solution was achieved by identifying and fixing critical bugs in the initial data loading and processing pipeline.

---

## 📖 The Challenge

The goal of the competition was to predict the spatial cellular organization from histology images. This translated to a multi-target regression problem: given a small image patch from a larger tissue slide, the model had to predict the values of 35 distinct biological markers.

**The primary metric was the average per-spot Spearman correlation coefficient.**

---

## 🛠️ Key Features & Technical Skills Demonstrated

This project showcases a complete, end-to-end deep learning workflow:

*   **Data Pipeline:**
    *   **Efficient Data Handling:** A custom `DataFactory` class was built to efficiently process metadata from large HDF5 files using vectorized Pandas operations.
    *   **On-the-Fly Patch Extraction:** A custom PyTorch `Dataset` class (`HESpotDataset`) extracts image patches on-the-fly, avoiding the need to store millions of small files.
    *   **Robust Caching:** An LRU (Least Recently Used) cache was implemented to keep frequently accessed whole-slide images in memory, significantly speeding up epoch times.
*   **Modeling & Training:**
    *   **Model Architecture:** Fine-tuned a pre-trained `ResNet18` model, replacing the final layer with a regression head that includes Dropout for regularization.
    *   **Modern Training Practices:** Utilized the `AdamW` optimizer, `MSELoss` for regression, and a `ReduceLROnPlateau` learning rate scheduler.
    *   **Robust Training Loop:** A modular `Trainer` class encapsulates the entire training and validation process, including early stopping based on the validation Spearman score and gradient clipping for stability.
*   **Systematic Debugging:**
    *   The core of this project was a deep dive into debugging a "silent" failure where the model was not learning effectively.
    *   Diagnosed and fixed critical data pipeline bugs related to **case-sensitive column names**, **incorrect data type handling** (`numpy.object_`), and **flawed data normalization**.

---

## ⚙️ How to Run This Project

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/your-username/kaggle-histology-image-regression.git
    cd kaggle-histology-image-regression
    ```

2.  **Set up the Environment:**
    It is recommended to use a virtual environment.
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```
    Install the required packages:
    ```bash
    pip install -r requirements.txt
    ```

3.  **Download the Data:**
    Download the competition data from the [Elucidata Global AI Hackathon '25 Kaggle Page](https://www.kaggle.com/competitions/el-hackathon-2025/data) and place it in a `/kaggle/input/` directory, or update the file paths in the notebook accordingly.

4.  **Run the Notebook:**
    Launch Jupyter and open the `your-notebook-name.ipynb` file. Run the cells sequentially to see the data preparation, training, and prediction process.
    ```bash
    jupyter notebook
    ```

---

## 💡 Key Takeaways

This project was a powerful lesson in moving beyond baseline models and into the critical, real-world skill of pipeline optimization. The main takeaways were:

1.  **Never Trust Your Data Pipeline:** Always write explicit diagnostic checks to verify data types, ranges, and shapes at every step.
2.  **Quantifiable Improvement is a Powerful Story:** The journey from a working model to a high-performing model is where the most valuable learning occurs.
3.  **Persistence Pays Off:** The final 28.7% score improvement was achieved after the competition had already ended, driven by a desire to understand the "why" behind the initial results.
