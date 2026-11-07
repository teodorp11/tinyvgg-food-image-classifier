# 🍕🥩🍣 TinyVGG Food Image Classifier

A **Convolutional Neural Network (CNN)** built from scratch in **PyTorch** that classifies food images into three classes: **pizza**, **steak**, and **sushi**.

The model is a replica of the **TinyVGG** architecture from the [CNN Explainer](https://poloclub.github.io/cnn-explainer/) website. It's trained on a small subset of the [Food101 dataset](https://data.vision.ee.ethz.ch/cvl/datasets_extra/food-101/).

---

## 📚 About This Project

This project is part of the **[PyTorch for Deep Learning Bootcamp](https://www.learnpytorch.io/)** course by **[Daniel Bourke](https://github.com/mrdbourke)**, specifically:

> **Section 04 – PyTorch Custom Datasets**
> 📖 Course material: [learnpytorch.io/04_pytorch_custom_datasets](https://www.learnpytorch.io/04_pytorch_custom_datasets/)
> 💻 Original repository: [mrdbourke/pytorch-deep-learning](https://github.com/mrdbourke/pytorch-deep-learning)

I wrote the notebook while following the course and added extra explanations, comments, and helper functions along the way.

---

## 🗂️ Project Structure

```text
tinyvgg-food-image-classifier/
├── classifier.ipynb     # Main notebook: data loading, model, training, evaluation & predictions
├── requirements.txt     # Python dependencies
├── .gitignore           # Files/folders excluded from Git
└── README.md            # Project documentation
```

> [!NOTE]
> The `data/` folder isn't included in this repository. The notebook downloads the dataset automatically.

---

## 📦 Dataset

The dataset is a subset of Food101 provided by the course:
**https://github.com/mrdbourke/pytorch-deep-learning/raw/main/data/pizza_steak_sushi.zip**

| Split | Pizza | Steak | Sushi | Total |
| :---: | :---: | :---: | :---: | :---: |
| Train |  78   |  75   |  72   | **225** |
| Test  |  25   |  19   |  31   | **75**  |

It uses the standard image classification folder layout, so it can be loaded with `torchvision.datasets.ImageFolder`:

```text
data/pizza_steak_sushi/
├── train/
│   ├── pizza/
│   ├── steak/
│   └── sushi/
└── test/
    ├── pizza/
    ├── steak/
    └── sushi/
```

---

## 🧠 Model Architecture (TinyVGG)

| Block | Layers | Output Shape |
| :--- | :--- | :---: |
| **Input** | RGB image resized to 64×64 | `[B, 3, 64, 64]` |
| **Conv Block 1** | Conv2d → ReLU → Conv2d → ReLU → MaxPool2d | `[B, 10, 32, 32]` |
| **Conv Block 2** | Conv2d → ReLU → Conv2d → ReLU → MaxPool2d | `[B, 10, 16, 16]` |
| **Classifier** | Flatten → Linear(2560 → 3) | `[B, 3]` |

- **Loss function:** `nn.CrossEntropyLoss`
- **Optimizer:** `torch.optim.Adam` (lr = 0.001)
- **Batch size:** 32
- **Epochs:** 35

---

## 🧪 Experiments

| Model | Description | Final Train Acc | Final Test Acc |
| :--- | :--- | :---: | :---: |
| **Model 0** | TinyVGG **without** data augmentation | ~77% | ~44% |
| **Model 1** | TinyVGG **with** data augmentation (`TrivialAugmentWide`) | ~55% | ~41% |

**Takeaways:**
- **Model 0** overfits: its training accuracy keeps going up while its test loss gets worse.
- **Model 1** overfits less because of data augmentation, but this small model and tiny dataset hold back accuracy for both.
- To improve results, you could add more data, train a larger model, or use **transfer learning**, which is covered in later course sections.

---

## 🚀 Getting Started

### Option A: Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/tinyvgg-food-image-classifier.git
cd tinyvgg-food-image-classifier

# 2. (Optional) Create and activate a virtual environment
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch Jupyter
jupyter notebook classifier.ipynb
```

When you run the notebook locally, use the **"Second Option"** cells, which download and store the data under `data/pizza_steak_sushi`.

### Option B: Run in Google Colab

1. Upload `classifier.ipynb` to [Google Colab](https://colab.research.google.com/).
2. Use the **"First Option"** cells. They mount Google Drive and store the dataset there permanently.
3. *(Recommended)* Turn on a GPU: `Runtime → Change runtime type → GPU`.

---

## 🔍 Features

- ✅ Downloads and extracts the dataset automatically (locally or in Google Drive)
- ✅ Device-agnostic code (CUDA / CPU)
- ✅ TinyVGG implementation with detailed, layer-by-layer comments
- ✅ Reusable `train_step`, `test_step` and `train` functions
- ✅ Loss and accuracy curves, plus a side-by-side comparison of the two models
- ✅ Predictions on custom images downloaded from the internet
- ✅ Predictions on random test images, with a bar chart showing **all class probabilities**

---

## 🛠️ Tech Stack

- [PyTorch](https://pytorch.org/) & [torchvision](https://pytorch.org/vision/stable/index.html)
- [torchinfo](https://github.com/TylerYep/torchinfo)
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [Jupyter](https://jupyter.org/)

---

## 🙏 Acknowledgements

- **[Daniel Bourke](https://github.com/mrdbourke)** for the excellent *PyTorch for Deep Learning Bootcamp* course and the dataset.
- **[CNN Explainer](https://poloclub.github.io/cnn-explainer/)** (Polo Club of Data Science, Georgia Tech) for the TinyVGG architecture.
- **[Food101](https://data.vision.ee.ethz.ch/cvl/datasets_extra/food-101/)** dataset authors (Bossard et al., ETH Zurich).

---

## ⚠️ Disclaimer

> [!IMPORTANT]
> The `README.md`, `.gitignore`, and `requirements.txt` files in this repository were **generated with Claude Opus 5.5** (an AI assistant). I reviewed them before publishing, but some details (for example, package versions or reported metrics) may still need adjusting.
>
> This is a personal **learning project** based on the course material listed above. It isn't affiliated with or endorsed by Daniel Bourke or Zero To Mastery.

