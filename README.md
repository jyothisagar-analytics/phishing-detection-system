# Phishing Detection System
### Hybrid Machine Learning Based on URL Analysis

A web-based phishing URL detection system built with Flask that uses a hybrid machine learning model to classify URLs as **safe or phishing** in real time. Users can sign up, log in, and test any URL through a clean web interface.

---

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [ML Models Used](#ml-models-used)
- [Setup & Installation](#setup--installation)
- [Usage](#usage)
- [Security Notes](#security-notes)
- [Reference](#reference)

---

## Overview

This system extracts **30 features** from any given URL — including domain age, WHOIS data, HTML content analysis, and URL structure — and passes them through a trained Gradient Boosting Classifier to determine the probability of the URL being a phishing site.

---

## Features

- Real-time phishing URL detection with probability score
- 30 URL and website features extracted automatically
- User authentication with OTP email verification
- SQLite database for user management
- Clean Flask web interface

---

## Project Structure

```
phishing-detection-system/
├── app.py              # Main Flask application & routes
├── feature.py          # 30-feature URL extraction class
├── flowchart.pdf       # System architecture flowchart

---

## How It Works

```
User enters URL
      ↓
Feature extraction (feature.py)
  - URL structure: length, IP usage, symbols, subdomains
  - Domain info: WHOIS, registration age, DNS records
  - HTML content: iframes, popups, form handlers, anchors
  - External: Google index, page rank, website traffic
      ↓
30 features passed to trained model (model.pkl)
      ↓
Gradient Boosting Classifier predicts
      ↓
Result displayed as safety percentage
```

---

## ML Models Used

| Model | Type |
|---|---|
| Logistic Regression | Base |
| Random Forest | Base |
| Decision Tree | Base |
| Support Vector Machine | Base |
| Naive Bayes | Base |
| Gradient Boosting | Base |
| LSD – Soft Voting | Hybrid (LR + SVC + DT) |
| LSD – Hard Voting | Hybrid (LR + SVC + DT) |
| LSD + GridSearchCV | Hybrid + Tuning |
| Stacking Classifier | Ensemble (RF + MLP + LightGBM) |

The final deployed model is the **Gradient Boosting Classifier**.

---

## Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/phishing-detection-system.git
cd phishing-detection-system
```

### 2. Create a virtual environment
```bash
python -m venv venv
source venv/bin/activate       # Windows: venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

Create a `.env` file in the root directory:
```
EMAIL_ADDRESS=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
```

> Use a Gmail **App Password** — generate one at https://myaccount.google.com/apppasswords

### 5. Initialize the database
```bash
python -c "
import sqlite3
con = sqlite3.connect('signup.db')
con.execute('CREATE TABLE IF NOT EXISTS info (user TEXT, email TEXT, password TEXT, mobile TEXT, name TEXT)')
con.commit()
con.close()
"
```

### 6. Run the app
```bash
python app.py
```

Visit: **http://127.0.0.1:5000**

---

## Usage

1. Open the app in your browser
2. Sign up with your email — you will receive an OTP for verification
3. Log in with your credentials
4. Enter any URL in the input box
5. The system returns a **safety percentage** — higher means safer

---

## Security Notes

- Never commit your `.env` file or credentials to GitHub
- `signup.db` contains user data — keep it out of version control (already in `.gitignore`)
- Passwords are currently stored as plain text — consider hashing with `bcrypt` for production

---

## Reference

Based on the paper:
**"Phishing Detection System Through Hybrid Machine Learning Based on URL"**

Extended with:
- Stacking Classifier (RF + MLP + LightGBM)
- Flask frontend with user authentication
- Ensemble methods beyond the base paper's RF/DT/SVM/NB models

---

## Author

> Sai Jyothi U
> Rao Bahadur Y. Mahabaleswarappa Engineering College
> AI&ML

---

## License

This project is for academic purposes only.
