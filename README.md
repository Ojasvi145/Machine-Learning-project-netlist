# Machine-Learning-project-netlist
# Hand-Drawn Electrical Circuit Recognition and Reconstruction via Machine learning
This repository contains the implementation of a robust system designed to automate the creation of simulation-ready schematic files directly from hand-drawn circuit sketches. By leveraging a hybrid Deep Learning and Heuristic pipeline, the project bridges the gap between physical conceptualization and digital simulation.
## 🚀 Overview
Engineers frequently draft initial circuit concepts using pencil and paper, but manually transforming these into simulation software is labor-intensive.  This project solves that by:

1.Locating and classifying hand-drawn components using the YOLO (You Only Look Once) model. 2.Mathematically predicting connection points (terminals) via a custom heuristic algorithm. 3.Extracting topology through wire skeletonization and node detection.
4.Generating a SPICE netlist for immediate use in industry-standard simulation tools. 

## 🛠️ Methodology
The pipeline is divided into four sequential phases:
1. Component Detection (YOLO)Utilizes the YOLO architecture to treat detection as a single regression problem, predicting bounding boxes and class probabilities directly from the image. Preprocessing: Includes Otsu's binarization and Gaussian blur to separate ink from background and reduce noise.
2. Heuristic Terminal EstimationInstead of using a secondary neural network, this system uses geometric rules to determine "invisible" terminal locations (pins).Mathematical Logic: Terminal coordinates $T$ are calculated based on the component class $C$ and bounding box midpoints. Example for Resistors/Capacitors/Inductors: $$T(C_{i}, B) = (x_{min}, y_{mid}), (x_{max}, y_{mid})$$
3. Topology ExtractionWire Skeletonization: Hand-drawn strokes are thinned to a single-pixel width to be treated as mathematical paths. Node Recognition: Identifies junctions by flagging pixels with more than two neighbors in the skeletonized image.
4. Reconstruction & Netlist GenerationThe visual data and connectivity logic are fused into a netlist graph $G=(V, E)$. This graph is then serialized into SPICE format (e.g., R1 1 2 10k). +1

## 📈 Performance
The system was evaluated using standard metrics, achieving an average F1-score exceeding 0.90. Key Achievements100% Node-Level Connectivity Accuracy: The system successfully associated every terminal with its respective node without open or short circuit errors.  
Real-Time Performance: The system is capable of running in real-time on Jetson hardware. 🎓 Authors: Ashi Sharma (BITS Pilani) Raghav Dhawan (BITS Pilani) Ojasvi Kaswan (BITS Pilani) 
