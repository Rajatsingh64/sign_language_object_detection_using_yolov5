# YOLOv5 - American Sign Language Classifier

This project uses YOLOv5 to classify American Sign Language (ASL) hand gestures, specifically the following gestures:

- Hello
- I Love You
- No
- Thanks
- Please
- Yes

The model is trained to recognize these ASL gestures from images.

## Prerequisites

- Python 3.8
- pip (Python package installer)

## Setup

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/your-username/yolov5.git
    cd yolov5
    ```

2. **Install Dependencies:**

    Make sure you are using Python 3.8. Then, install the required dependencies.

    ```bash
    pip install -r requirements.txt
    ```

3. **Label the Data:**

    We use the `labelImg` tool to annotate images for training.

    - Install `labelImg`:
      ```bash
      pip install labelImg
      ```

    - Open the tool and annotate images of the ASL gestures. Save annotations in YOLO format (i.e., `.txt` files with class and coordinates).
    
    - Example of a label file:
        ```
        0 0.5 0.5 0.2 0.3
        ```
        The numbers correspond to the class (0 for Hello, 1 for I Love You, etc.), followed by normalized center coordinates and width/height of the bounding box.

4. **Prepare Dataset:**

    Organize your dataset into the following folder structure:

    ```
    yolov5/
    ├── data/
    │   ├── images/
    │   │   ├── train/
    │   │   └── val/
    │   └── labels/
    │       ├── train/
    │       └── val/
    ├── models/
    └── train.py
    ```

    - Place your training and validation images in `data/images/train/` and `data/images/val/`.
    - Place the corresponding annotation files (e.g., `.txt`) in `data/labels/train/` and `data/labels/val/`.

5. **Train the Model:**

    To train the model, run the following command:

    ```bash
    python train.py --img 640 --batch 16 --epochs 50 --data data.yaml --weights yolov5s.pt
    ```

    Here, `data.yaml` is the configuration file that contains paths to the dataset and class labels. You can create a `data.yaml` like this:

    ```yaml
    train: data/images/train
    val: data/images/val
    nc: 6
    names: ['Hello', 'ILoveYou', 'No', 'Thanks', 'Please', 'Yes']
    ```

6. **Predict using the Model:**

    After training, you can use the model to make predictions on new images:

### Make sure to move run.py and best.pt inside yolov5 clone directory
    
    ```bash
    python detect.py --weights runs/train/exp/weights/best.pt --img 640 --source path_to_your_image_or_directory
    ```

    Replace `path_to_your_image_or_directory` with the path to the image or directory where you want to perform predictions.

## Example Usage

To predict an image (e.g., `test.jpg`):

```bash
python detect.py --weights runs/train/exp/weights/best.pt --img 640 --source test.jpg
