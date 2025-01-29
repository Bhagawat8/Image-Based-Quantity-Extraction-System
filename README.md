# Image-Based Quantity Extraction System

This project implements an end-to-end pipeline that extracts quantitative values (e.g., 100 milligram, 500 gram) from images. The system is designed to identify quantities mentioned in product images, making it particularly useful for use cases such as e-commerce, healthcare, and content moderation where precise product information is vital. By combining Optical Character Recognition (OCR) with Named Entity Recognition (NER), this project accurately extracts numerical data from text embedded in images.

---

## Features

- **Image Input:** Accepts product images as input.
- **OCR Integration:** Uses state-of-the-art OCR to extract text from images.
- **NER for Quantities:** Fine-tuned model for extracting specific quantities like volume (ml, L), weight (g, kg), dimensions (cm, mm), and more from the OCR-extracted text.
- **Accurate Outputs:** Returns the detected quantity in a standardized format (e.g., 12.5 centimetre).
- **Scalable:** Designed for scalability in processing large datasets of images.

---

## Workflow

1. **Input:** An image of a product containing text (e.g., labels, packaging).
2. **OCR Processing:**
   - The OCR model extracts raw text from the image.
   - Post-processing cleans the text by removing unwanted characters and formatting issues.
3. **Named Entity Recognition (NER):**
   - The fine-tuned NER model identifies and extracts quantities (e.g., 100ml, 1.5kg, 12.5 centimetre) from the processed OCR output.
4. **Output:** The system returns the identified quantity in text format.

---

## Data Description

The dataset consists of the following columns:

1. `index`: A unique identifier (ID) for the data sample.
2. `image_link`: Public URL where the product image is available for download (e.g., `https://m.media-amazon.com/images/I/71XfHPR36-L.jpg`). Images can be downloaded using the `download_images` function from `src/utils.py`.
3. `group_id`: Category code of the product.
4. `entity_name`: Product entity name (e.g., `item_weight`).
5. `entity_value`: Product entity value (e.g., `34 gram`). **Note:** For `test.csv`, this column is not available as it is the target variable.

---

## Output Format

The output file should be a CSV with the following columns:

1. `index`: The unique identifier (ID) of the data sample. This index should match the test record index.
2. `prediction`: A string in the format `x unit`, where `x` is a float number in standard formatting, and `unit` is one of the allowed units. Ensure the two values are concatenated with a space between them.

### Valid Examples:
- `2 gram`
- `12.5 centimetre`
- `2.56 ounce`

### Invalid Examples:
- `2 gms`
- `60 ounce/1.7 kilogram`
- `2.2e2 kilogram`

If no value is found in the image for any test sample, return an empty string (`""`). Ensure the number of output samples matches `test.csv`; otherwise, the output will not be evaluated.

---

## Technology Stack

- **OCR Model:** Florence-2-large-ft for text extraction.
- **NER Model:** Fine-tuned T5-base model for extracting quantitative entities.
- **Libraries & Frameworks:**
  - Python
  - Transformers (Hugging Face)
  - Pandas, NumPy
  - Matplotlib, Seaborn (for data visualization)
  - Jupyter Notebooks

---

## Installation

Follow the steps below to set up the project locally:

1. Clone the Repository:
   ```sh
   git clone https://github.com/Bhagawat8/Image-Based-Quantity-Extraction-System.git
   cd quantity-extraction
   ```
2. Download Pretrained Models:
   - **OCR Model:** Florence-2-large-ft ([Download Link](https://huggingface.co/microsoft/Florence-2-large-ft))
   - **NER Model:** Fine-tuned T5-base ([Download Link](https://drive.google.com/drive/folders/1qBvsh-yheqe7x3LzOafUMbvUOJwHmHrn?usp=sharing))
3. Set Up Environment: Create a `.env` file for environment variables if necessary (e.g., API keys for cloud-based OCR services).

---

## Future Enhancements

- Support for additional languages in OCR.
- Extension to other types of entities (e.g., dimensions, expiry dates).
- Real-time processing capability.
- Integration with a web interface for user-friendly interaction.

---

## License

This project is licensed under the **MIT License**. See the `LICENSE` file for more details.

---

## Acknowledgements

- **Hugging Face** for the T5-base model.
- **Microsoft** for the Florence-2-large-ft OCR model.
- **Open-source contributors** for libraries and tools used in this project.
