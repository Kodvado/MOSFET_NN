# MOSFET Neural Network Modeling

## Overview

This project explores the use of neural networks to model and characterize MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor) behavior. [cite: 24, 25, 26, 27] It demonstrates a novel approach to address the limitations of traditional MOSFET modeling techniques, such as SPICE, by leveraging neural networks to predict key device characteristics. [cite: 24, 25, 26, 27] The project focuses on predicting drain current ($I_{D}$), threshold voltage ($V_{th}$), and transconductance parameter ($K_{P}$) using both synthetic and experimental data. [cite: 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57]

## Motivation

Traditional MOSFET modeling with SPICE involves challenges like:

* Computational cost and complexity, especially at nanometer scales. [cite: 28, 42, 43, 44, 45, 46, 47]
* Difficulties in parameter extraction. [cite: 42, 43, 44, 45, 46, 47, 52, 53]
* Discrepancies between simulated and real-world device behavior. [cite: 49, 50, 51]

This project aims to address these by using neural networks to learn MOSFET behavior directly from data, automating parameter extraction, and improving accuracy. [cite: 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57]

## Methodology

The project is divided into four phases:

* **Phase 1:** Training a neural network on a public MOSFET dataset to predict drain current ($I_{D}$). [cite: 302, 303, 304]
* **Phase 2:** Training neural networks on experimental I-V data from commercial MOSFETs. [cite: 203, 204, 205, 206, 207, 208, 209, 210, 211, 212, 213, 214, 215]
* **Phase 3:** Generating synthetic datasets using SPICE simulations with Level 1 and Level 3 MOSFET models. [cite: 228, 229, 230, 231, 232, 233, 234, 235, 236, 237, 238, 239, 240, 241, 242, 243, 244, 245, 246, 247, 248, 249, 250, 251]
* **Phase 4:** Training neural networks to extract threshold voltage ($V_{TO}$) and transconductance parameter ($K_{P}$) from the synthetic datasets. [cite: 264, 265, 266, 267, 268, 269, 270, 271, 272, 273, 274, 275, 276, 277, 278, 279, 280, 281, 282, 283, 284, 285]

## Results

* **Phase 1:** Achieved $R^{2}$ of 0.99995 in predicting drain current from a public dataset. [cite: 304, 305, 306, 307, 308, 309, 310, 311]
* **Phase 2:** Demonstrated high accuracy ($R^{2}$ \> 0.998) in predicting drain current from experimental data across five commercial NMOS devices. [cite: 313, 314, 315, 316, 317, 318, 319, 320, 321, 322, 323, 324, 325, 326, 327]
* **Phase 3:** Generated large synthetic datasets using Level 1 (50,000 devices) and Level 3 (55,000 devices) SPICE models. [cite: 327, 328, 329, 330, 331, 332, 333, 334, 335, 336, 365, 366, 367, 368, 369, 370, 371, 372, 373, 374, 375, 376, 377, 378, 379, 380, 381]
* **Phase 4:** Successfully trained neural networks to extract $V_{TO}$ (e.g., $R^{2}$ = 0.9980 for Level 1) and $K_{P}$ (e.g., $R^{2}$ = 0.9695 for Level 3). [cite: 337, 338, 339, 340, 341, 342, 343, 344, 345, 381, 382, 383, 384, 385, 386, 387, 388, 389, 390, 391, 392, 393, 394, 395, 396, 397, 398, 399, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 418, 419, 420, 421]

## Usage

To use this code:

1.  **Installation:**
    * Install the required libraries (e.g., TensorFlow, PySpice)
    ```bash
    pip install tensorflow pyspice numpy pandas scikit-learn
    ```
2.  **Data:**
    * Prepare your MOSFET data in CSV format.
    * Ensure the data includes the necessary parameters ($V_{GS}$, $V_{DS}$, $I_{D}$).
3.  **Scripts:**
    * Use the provided Python scripts to train the neural networks and perform predictions or parameter extraction.
    * Modify the script parameters as needed (e.g., file paths, training parameters).

## File Structure
