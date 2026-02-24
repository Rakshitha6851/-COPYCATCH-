# CopyCatch

CopyCatch is a web-based plagiarism detection tool designed for educators to check student assignments for similarity. It supports various file formats including PDFs, DOCX, TXT files, and images (scanned/handwritten assignments). The application uses advanced text extraction techniques, including OCR for images, and computes similarity scores using TF-IDF vectorization and cosine similarity.

## Features

- **Multi-format Support**: Accepts PDF, DOCX, TXT, and image files (PNG, JPG, JPEG)
- **Intelligent Image Validation**: Filters out non-assignment images (e.g., photos of people or objects) using face detection
- **OCR Integration**: Extracts text from scanned documents and handwritten assignments
- **Fast Similarity Detection**: Uses TF-IDF and cosine similarity with parallel processing
- **Caching System**: Caches extracted text to improve performance on repeated uploads
- **Web Interface**: Simple Flask-based web application with modern UI
- **Grouping Results**: Groups similar assignments and highlights plagiarism cases

## Installation

### Prerequisites

- Python 3.7+
- Tesseract OCR (for text extraction from images)
- Git (optional, for cloning)

### Install Dependencies

1. Clone or download the project:
   ```bash
   git clone <repository-url>
   cd COCPYCATCH
   ```

2. Install Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Install Tesseract OCR:
   - **Windows**: Download from [https://github.com/UB-Mannheim/tesseract/wiki](https://github.com/UB-Mannheim/tesseract/wiki) and add to PATH
   - **macOS**: `brew install tesseract`
   - **Linux**: `sudo apt-get install tesseract-ocr`

4. Download language data for Tesseract (English):
   ```bash
   # This is usually included with Tesseract installation
   ```

## Usage

1. Run the application:
   ```bash
   python app.py
   ```

2. Open your browser and navigate to `http://localhost:5000`

3. Complete the CAPTCHA on the landing page

4. Upload student assignment files (minimum 2 files, maximum 64 files)

5. Click "Upload & Check Similarity"

6. View the results page showing similarity groups and scores

## How It Works

1. **File Upload**: Students' assignments are uploaded via the web interface
2. **Validation**: Images are validated to ensure they contain text-based assignments (not photos)
3. **Text Extraction**:
   - PDFs: Direct text extraction with OCR fallback
   - DOCX: Paragraph text extraction
   - TXT: Direct reading
   - Images: OCR using Tesseract
4. **Preprocessing**: Text is normalized (lowercased, whitespace cleaned)
5. **Similarity Analysis**:
   - TF-IDF vectorization with limited vocabulary for performance
   - Cosine similarity computation
   - Grouping of similar documents (threshold: 70% similarity)
6. **Results**: Displays grouped similar assignments with average similarity scores

## Project Structure

```
COCPYCATCH/
├── app.py                 # Main Flask application
├── static/
│   └── style.css          # CSS styles
├── templates/
│   ├── captcha.html       # Landing page with CAPTCHA
│   ├── upload.html        # File upload page
│   ├── results.html       # Results display page
│   └── uploadpdf.html     # Alternative upload page
├── uploads/               # Temporary upload directory
├── cache/                 # Cached extracted text
└── TODO.md                # Development notes
```

## Dependencies

- Flask: Web framework
- OpenCV: Computer vision for image validation
- Pillow: Image processing
- Pytesseract: OCR engine
- Scikit-learn: Machine learning for similarity computation
- PyMuPDF (fitz): PDF text extraction
- python-docx: DOCX text extraction

## Configuration

- **Similarity Threshold**: Currently set to 0.7 (70%) - can be adjusted in `app.py`
- **Max Files**: Limited to 64 files per upload
- **Supported Formats**: PDF, DOCX, TXT, PNG, JPG, JPEG
- **Cache**: Text extraction results are cached for performance

## Security Notes

- The application includes basic image validation to prevent misuse
- Uploaded files are temporarily stored and processed server-side
- No persistent data storage (results are session-based)

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is open-source. Please check the license file for details.

## Support

For issues or questions, please create an issue in the repository or contact the maintainers.
