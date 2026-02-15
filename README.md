# 🎵 Mashup Generator

An automated Flask web application that creates audio mashups by downloading tracks from YouTube, intelligently trimming and merging them, then delivering the final product directly to your inbox.

**Tech Stack:** Flask · yt-dlp · pydub · Flask-Mail · FFmpeg

**Live Demo:** https://mashup-assign7.onrender.com/

---

## ✨ What It Does

The Mashup Generator streamlines the process of creating audio compilations:

1. **Smart Search** - Queries YouTube for your chosen artist/singer
2. **Batch Download** - Retrieves audio from multiple top-ranked videos
3. **Precision Trimming** - Cuts each track to your specified duration
4. **Seamless Merging** - Concatenates clips into a polished mashup
5. **Automated Delivery** - Packages and emails the final product as a zip archive

All through a clean, simple web interface.

---

## 📁 Project Structure

```
Mashup_Assign7/
│
├── app.py                  # Core Flask application logic
├── requirements.txt        # Python package dependencies
├── Procfile               # Gunicorn deployment configuration
├── .python-version        # Recommended Python runtime
│
└── templates/
    ├── index.html         # Main submission form
    └── success.html       # Confirmation/error page
```

---

## 🚀 Quick Start

### System Requirements

- **Python:** 3.8 or higher
- **FFmpeg:** System-level installation required

#### Installing FFmpeg

```bash
# macOS (Homebrew)
brew install ffmpeg

# Ubuntu/Debian
sudo apt update && sudo apt install -y ffmpeg

# Windows
# Download from https://ffmpeg.org/download.html
# Add to system PATH
```

### Local Setup

1. **Clone and navigate:**
   ```bash
   git clone https://github.com/hardik-kumar-10/Mashup_Assignment7.git
   cd Mashup_Assignment7
   ```

2. **Set up virtual environment:**
   ```bash
   python -m venv venv
   
   # Activate (macOS/Linux)
   source venv/bin/activate
   
   # Activate (Windows PowerShell)
   .\venv\Scripts\Activate.ps1
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure SMTP credentials:**
   
   The application requires email configuration via environment variables:
   
   ```bash
   # macOS/Linux
   export MAIL_USERNAME="your-email@example.com"
   export MAIL_PASSWORD="your-app-password"
   
   # Windows PowerShell
   $env:MAIL_USERNAME="your-email@example.com"
   $env:MAIL_PASSWORD="your-app-password"
   ```
   
   **Gmail Users:** Enable 2FA and generate an App Password through your Google Account settings. Never commit credentials to version control.

5. **Launch the application:**
   ```bash
   # Development mode
   python app.py
   
   # Production with Gunicorn
   gunicorn app:app
   ```

Access the app at `http://localhost:5000`

---

## 💡 How to Use

Visit the web interface and complete the form with these parameters:

| Field | Description | Validation |
|-------|-------------|------------|
| **Singer Name** | Artist or search query for YouTube | Free text |
| **Number of Videos** | Quantity of tracks to download | Must exceed 10 |
| **Duration (seconds)** | Length of each audio clip | Must exceed 20 |
| **Email Address** | Delivery destination for mashup | Valid email format |

**Processing Flow:**
The system searches YouTube → downloads top N audio tracks → trims each to specified duration → merges into `mashup.mp3` → compresses to `mashup.zip` → emails attachment → removes temporary files

**Response Handling:**
- Validation errors display immediately
- Success confirmation appears after email dispatch
- Generic errors reported for processing failures

---

## ☁️ Production Deployment

### Heroku & Similar Platforms

1. **Prepare repository:**
   ```bash
   git init
   git add .
   git commit -m "Initial deployment"
   ```

2. **Platform configuration:**
   - The included `Procfile` specifies: `web: gunicorn app:app`
   - Set `MAIL_USERNAME` and `MAIL_PASSWORD` as environment variables in platform dashboard

3. **FFmpeg requirement:**
   - Heroku: Add the community FFmpeg buildpack
   - Render/Railway: Usually pre-installed
   - Custom servers: Install via package manager

---

## 🔧 Troubleshooting

### Common Issues & Solutions

**FFmpeg not detected**
- Verify installation: `ffmpeg -version`
- Ensure FFmpeg is in system PATH
- Restart terminal/IDE after installation

**"No audio downloaded" error**
- Search query may be too specific or returning no results
- Try broader search terms
- Check internet connectivity and YouTube availability

**yt-dlp download failures**
- Some videos restricted by region or DRM
- App continues processing available videos
- Increase video count to compensate for failures

**SMTP authentication errors**
- Double-check `MAIL_USERNAME` and `MAIL_PASSWORD` values
- Gmail requires App Password with 2FA enabled
- Verify email provider allows SMTP access
- Check for typos in environment variables

**Performance issues with large jobs**
- Multiple downloads consume significant bandwidth and time
- Consider implementing job queues (RQ, Celery)
- Monitor server memory and timeout limits

---

## ⚖️ Legal & Ethical Considerations

**Important Notice:** This tool downloads content from YouTube programmatically. Users must:

- Comply with YouTube's Terms of Service
- Respect copyright laws and intellectual property rights
- Use downloaded content within legal fair use boundaries
- Obtain necessary permissions for commercial use

**This project is provided for educational purposes only.**

**Security Warning:** The application lacks authentication, rate limiting, and abuse protection. Do not expose to public internet without implementing proper security controls, user quotas, and monitoring.

---

## 🎯 Future Enhancement Ideas

- **Job Queue Integration** - Implement RQ or Celery for background processing with progress tracking
- **User Authentication** - Add login system with per-user quotas and usage analytics
- **Direct Downloads** - Provide in-browser download option alongside email delivery
- **Advanced Audio Effects** - Support crossfading and other transition effects between clips
- **Cloud Storage** - Upload results to S3/GCS instead of email attachments
- **API Endpoints** - Expose programmatic access for integrations
- **Admin Dashboard** - Monitor system usage, errors, and performance metrics

---

## 📄 License

This project is open source. Please review the repository for license details.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page.
