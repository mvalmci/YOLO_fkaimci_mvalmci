# Custom Object Detector Project

## 1. Project Description

You will train a custom **YOLO object detection model** that can recognize 3 - 6 object classes of your own choosing, using free GPU resources on Google Colab.

**What you'll do:**
1. Choose 3-6 object classes -- your choice, within the constraints below.
2. Photograph and label a training dataset.
3. Train a model in Google Colab using the provided notebook.
4. Test your model and submit your results.

**What you'll learn:** the practical ML workflow (data collection, labeling, training, evaluation), why dataset quality matters more than model tweaking, and how to work with a cloud GPU environment.

**What you will NOT need to do:** write training code, tune hyperparameters extensively, or debug deep learning internals. The notebook handles training, your job is mainly building a good dataset and following the steps correctly.

**Project timeline:**

| Deadline | Deliverable |
|---|---|
| Friday, 09.10.2026 | Team Formation Notification |
| Friday, 16.10.2026 | Object Classes |
| Friday, 15.11.2026 | Dataset complete and labeled |
| December/ January | Presentation of implementation and results |

---

## 2. Student Checklist (read this before you start!)

Follow this order. Most wasted time comes from skipping ahead or working in the wrong tool at the wrong time.

**Before touching Colab:**
- Pick your classes and get them approved (see Requirements below)
- Take your photos (see minimum dataset spec below)
- Label your images using LabelStudio (https://labelstud.io/)
- Zip your dataset into the required folder structure (`images/` + `labels/` + `classes.txt`)

**In Google Colab:**
- Open the notebook link, sign in with your Google account, and **make a copy into your drive**.
- **Enable the GPU first**: `Runtime > Change runtime type > GPU`. If you skip this, training will silently run on CPU and take hours instead of minutes.
- Upload your zipped dataset
- Edit the cell that sets the number of classes and class names. This must exactly match your `classes.txt`
- Run cells **in order, top to bottom**. Do not skip cells or jump around.
- Wait for training to finish. Fo not close the browser tab or let the machine sleep during this
- Check the results cell/`results.png`. If accuracy (mAP50) is very low, see the Troubleshooting note below before assuming something is broken
- Download `best.pt` **before** you close the Colab tab or the session disconnects. Colab deletes everything when the session ends

**Common time-wasters to avoid:**
- Forgetting to enable the GPU (10x+ slower training)
- Not downloading `best.pt` before the session times out, having to retrain from scratch
- Labeling inconsistently (e.g. loose/sloppy boxes), poor accuracy that looks like a "broken" model
- Photographing all images from the same angle/background, model that looks fine in training but fails on new images
- Editing cells you weren't told to edit, or running cells out of order

**If your mAP50 stays below ~0.5 after training:** it's almost always a dataset problem (too few images, inconsistent labels, or classes that look too similar), not a bug in the notebook. Add more varied images before re-training rather than changing training parameters.

---

## 3. Requirements \& Hints

- **Classes:** choose 3-6 classes. Objects must be *visually distinct* from each other (avoid classes that look nearly identical, e.g. "red apple" vs. "red ball". That's a harder problem than this project is designed for).
- **No restricted subjects:** no people/faces, no weapons, no anything requiring special permissions.
- **Labeling tool:** use Label Studio and export in the exact format required by the notebook.
- Take pictures with a quality that matches the quality of pictures that will be used for object detection later. In other words: Don't use high quality for training, and low quality for testing.
- **Folder/zip structure:** must match the template exactly (an `images/` folder, a `labels/` folder, a `classes.txt` file).
- **Only edit the cells you're told to edit** in the Colab notebook, leave everything else as-is.
- **Standardized submission format:** every student submits a single zip containing:
  - `classes.txt`
  - `best.pt`
  - a screenshot of `results.png` (the training curves)

---

## 4. Minimum Dataset Size & Quality

| Requirement | Minimum |
|---|---|
| Number of classes | 3-6 |
| Images per class | at least 60-80 (aim for 100+ if possible) |
| Total dataset size | ~200-400 images minimum |
| Image variety | multiple backgrounds, angles, and lighting conditions per class, not just one setting |
| Distractor objects | include some images with *other* random objects present, so the model learns what *not* to detect |
| Occlusion | include some images where the target object is *partially* occluded (blocked by another object, a hand, overlapping with another instance, etc.), this teaches the model to still detect objects that aren't fully visible, which is common in real-world use |
| Image quality | in-focus, reasonably lit, object clearly visible |
| Labeling | every instance of the target object boxed tightly in every image; no missed or sloppy boxes |

---

## 5. Grading Scheme

### Minimum Requirements (60%)

- Fully labeled training dataset (meets the minimum size/quality spec above)
- Model is successfully trained (training completes, `results.png`/mAP shows reasonably good results: not necessarily high accuracy, but evidence the process worked correctly)
- Model can be run on a new image and produces correct output

### To move toward 100%:

- **Live video feed detection:** run the classifier in on a webcam and video file instead of a single static image.
- **Add computations on top of detections:** use the classes/boxes the model outputs to compute something meaningful. Ideas (be creative and implement your ideas):
  - Count objects per class and display a running tally on-screen (e.g. "3 apples, 1 banana")
  - Track objects across frames and count unique objects seen over time (e.g. count objects crossing a line, classic "people/car counting" pattern)
  - Compute and display simple relationships between detected objects, e.g. distance between two objects, or which objects are touching/overlapping
  - Log every detection with a timestamp to a CSV file, then plot detection frequency over time
  - Build a small heatmap of *where* detections occur most often in the frame over a video

### Other possibilities to boost your grade:

- **Move from Colab to local training and deployment:** set up GPU training locally and run inference without depending on Colab at all.
- Deploy and run on a Raspberry Pi or a similar embedded device.
- Deploy on a mobile device (Android/iOS)
- Compare model sizes (`yolo11n` vs `yolo11s` vs `yolo11m`) on speed vs. accuracy and report the trade-off

## 6. Links

Tutorial Video:
https://youtu.be/r0RspiLG260?si=E0jfYbQDh6uoDKNY

Google Colab:
https://colab.research.google.com/github/EdjeElectronics/Train-and-Deploy-YOLO-Models/blob/main/Train_YOLO_Models.ipynb

Label Studio:
https://labelstud.io/
