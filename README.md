# in2Pages APP:

## Overview

This project, developed as a group assignment for the Advanced Machine Learning course (2758) at Nova School of Business & Economics, introduces **in2Pages Magazine**. It's designed as a seamless one-stop web-app to help Gen-Z create personalized, community-based print magazines. The core innovation lies in rethinking how digital content transforms into lasting memories through a unique blend of digital and analog media.

## Team

The "in2Pages Magazine" project was developed by a team of MSc Business Analytics students:

*   **Jan Felix Specht** (64725)
*   **Marco Piccolo** (63996)
*   **Paul Beudert** (61533)
*   **Luis Soares** (64376)
*   **Stella Schwertner** (68369)

## in2Pages

in2Page offers a platform that helps users create personalized, community-based print magazines through a seamless web-app.

## AI Integration: PDF Content Moderation System

To ensure a safe and respectful platform, in2Pages integrates an ML-powered PDF Content Moderation System.

### Description
This system screens user-submitted content (text and images within PDFs) before publication, maintaining safety and trust without requiring extensive manual review.

### Objectives
*   Prevent offensive, disrespectful, or inappropriate content.
*   Foster a respectful digital environment.
*   Replace manual review processes to support large volumes of content.

### Moderation Pipeline

The moderation process involves several stages:

1.  **User Uploads Content (PDF):** Via an HTTP POST endpoint.
2.  **Parsing Layer (PyMuPDF):** Extracts text blocks and embedded images from the PDF.
3.  **Text & Image Moderation Models:**
    *   **Text Flow:**
        *   `fastText (LID)` for Language Identification (detects non-English content).
        *   `NLLB-200` for Text Translation (if non-English).
        *   `KoalaAI/Text-Mod.` probabilities for multi-label text toxicity detection.
    *   **Image Flow:**
        *   `CLIP (VIT-B)` embeds bitmaps & prompts.
        *   Similarity-based label selection.
4.  **Fusion & Logging:** Combines text and image moderation results (e.g., using pandas and saving to GDrive).
5.  **Decision Returned to User:** Based on moderation results (e.g., approve or flag for re-upload).

### Development Approach

The development followed a phased approach:

*   **Local Prototyping:** Initial parsing and text moderation (unitary/toxic-bert) were tested locally. Image moderation (SafeSearch API) faced cloud authentication issues.
*   **Scaling via Google Colab:** Moved to Colab for GPU access, fixed Flask-ngrok for stable tunnels, and refactored the Flask backend.
*   **Final Moderation Pipeline:** Integrated `lid.176.bin` for fastText Language ID, `NLLB-200` for translation, and `KoalaAI` for multi-label text moderation. For images, `CLIP (VIT-B/32)` was used.

## Testing via Webapp

The moderation system was tested through a web application.

*   **Process:** Running the script, opening the webapp, uploading a PDF.
*   **Result Example:** The webapp displays detected languages (e.g., en, de, fr) and provides text analysis (e.g., "Label: hate (H) (49%)" with an excerpt of offensive text). Image analysis provides flags (e.g., "a nudity scene") or confirms "None".

