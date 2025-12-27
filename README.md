# Neurobloom - Educational Assessment Platform

A comprehensive web-based platform for learning disorder assessment and prediction using interactive games and ML-powered analysis.

## 📁 Project Structure

```
Neurobloom/
├── app.py                          # Main Flask application
├── assessment_routes.py            # Assessment API endpoints
├── disorder_predictor.py           # ML prediction engine
│
├── templates/                      # HTML templates
│   ├── base.html                   # Base template
│   ├── login.html                  # Login page
│   ├── signup.html                 # Registration page
│   ├── index.html                  # Home page
│   ├── student.html                # Student dashboard
│   ├── faculty.html                # Faculty dashboard
│   ├── assessments_list.html       # Assessment listing
│   ├── assessment_test.html        # Text-based assessment
│   ├── assessment_visual.html      # Visual assessment
│   ├── assessment_results.html     # Results for traditional assessments
│   ├── dyslexia_integrated.html    # Dyslexia interactive games
│   ├── dyslexia_results.html       # Dyslexia results viewer
│   └── support.html                # Support page
│
├── static/                         # Static assets
│   ├── css/                        # Stylesheets
│   │   ├── index.css
│   │   ├── login.css
│   │   ├── signup.css
│   │   ├── student.css
│   │   ├── assessment.css
│   │   ├── assessment_results.css
│   │   └── assessment_landing.css
│   ├── js/                         # JavaScript files
│   ├── imgs/                       # Images
│   └── uploads/                    # User uploads
│
├── ml_models/                      # Machine learning models
│
├── Dyslexia_test/                  # Standalone dyslexia test system
│   ├── app.py
│   ├── model.py
│   ├── results_dyslexia.db
│   ├── static/
│   └── templates/
│
├── Dyscalculia_test/               # Standalone dyscalculia test system
│
└── .venv/                          # Virtual environment
```

## 🎯 Key Features

### Student Portal
- **User Registration & Login**: Secure authentication with password hashing
- **Profile Management**: Complete class and faculty setup
- **Assessment Dashboard**: View available assessments
- **Interactive Assessments**: 
  - Text-based questions
  - Visual/puzzle-based questions
  - Dyslexia playful screener (6 interactive games)
- **Results Viewing**: Attempt-by-attempt result viewing with analysis
- **Progress Tracking**: View performance across multiple assessments

### Assessment Types

#### 1. **Dyslexia Assessment** (ID=1)
- **Format**: Interactive playful screener with 6 games
- **Games**:
  - 🔤 Phoneme Detective - Delete first sound from words
  - 📝 Letter-Sound Match - Match letters to sounds
  - 🎵 Rhyme Finder - Identify rhyming words
  - 🔀 Unscramble Words - Decode scrambled letters
  - ❓ Real or Made-up? - Lexical decision task
  - ⚡ Fast Name - Rapid naming speed test
- **Scoring**: ML-based risk assessment algorithm
- **Risk Levels**: No risk likely, Low risk, Medium risk, High risk
- **Results Display**: Attempt-wise viewing with detailed breakdown

#### 2. **Dyscalculia Assessment** (ID=2)
- Traditional question-based assessment
- 20 mathematical reasoning questions

#### 3. **Dysgraphia Assessment** (ID=3)
- Traditional question-based assessment
- 20 writing/language questions

### Faculty Portal
- **Student Management**: View and manage students
- **Assessment Oversight**: Monitor student progress
- **Class Management**: Organize students by class/department

### Backend Systems
- **ML Prediction Engine**: Analyzes assessment responses for disorder risk
- **Result Storage**: Comprehensive JSON-based result storage
- **API Framework**: RESTful endpoints for all operations
- **Session Management**: Secure student/faculty sessions

# BTech

## 🗄️ Database Tables

### Core Tables
- **users**: Student and faculty accounts
- **assessment_types**: Available assessments (dyslexia, dyscalculia, dysgraphia)
- **questions**: Assessment questions
- **answer_options**: Multiple choice options
- **student_assessments**: Assessment session tracking
- **student_answers**: Individual question responses
- **assessment_results**: Detailed game results (dyslexia)
- **ml_predictions**: ML-based risk predictions
- **student_progress**: Aggregate performance metrics
- **faculty_notes**: Faculty observations

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- MySQL/MariaDB
- Flask
- mysql-connector-python

### Installation

1. **Clone and Setup Environment**
```bash
cd "d:\BTech Project\Project"
python -m venv .venv
.venv\Scripts\activate
```

2. **Install Dependencies**
```bash
pip install flask mysql-connector-python werkzeug
```

3. **Configure Database**
- Ensure MySQL is running
- Default credentials: root (no password)
- Database: neurobloom
- Port: 3306

4. **Run Application**
```bash
python app.py
```

Visit `http://localhost:5000`

## 📊 API Endpoints

### Authentication
- `POST /login` - User login
- `POST /signup` - New user registration
- `GET /logout` - User logout

### Assessment Management
- `GET /assessments` - List available assessments
- `POST /api/student-assessment/start` - Start new assessment
- `GET /api/assessment/<id>` - Get assessment details
- `POST /api/student-answers` - Submit answers
- `GET /assessment/results/<id>` - View results

### Dyslexia Specific
- `POST /api/analyze-dyslexia` - Analyze game results
- `POST /api/submit-assessment` - Save assessment results
- `GET /api/dyslexia-results/<id>` - Get all attempts
- `GET /dyslexia-results/<id>` - View results page

### Student Info
- `GET /api/student-info` - Get student profile
- `POST /api/setup-profile` - Complete profile setup
- `GET /api/student-stats` - Get dashboard statistics

## 🎮 Using Dyslexia Assessment

### For Students
1. Login to account
2. Go to Assessments page
3. Click "Start Assessment" on Dyslexia Assessment Test
4. Complete all 6 interactive games with audio prompts
5. Receive immediate risk assessment
6. Submit results to save
7. Click "View Results" to see attempt history

### For Faculty
1. Login as faculty
2. Monitor student progress on faculty dashboard
3. Review assessment results for assigned students

## 🔒 Security Features
- Password hashing with werkzeug
- Session-based authentication
- User role verification (student/faculty/admin)
- SQL injection prevention with parameterized queries
- CORS-ready API structure

## 📈 ML Prediction Model

The `disorder_predictor.py` implements predictive analysis:
- Analyzes question response patterns
- Calculates risk scores based on weighted factors
- Generates recommendations for intervention
- Stores predictions for progress tracking

### Dyslexia Scoring Algorithm
- **Phoneme Delete**: 1.6x weight (phonological awareness)
- **Letter-Sound**: 1.5x weight (letter-sound mapping)
- **Rhyme Recognition**: 1.2x weight (phonological processing)
- **Word Scramble**: 1.3x weight (word decoding)
- **Lexical Decision**: 1.2x weight (word recognition)
- **Rapid Naming**: 1.4x weight (naming speed)

Risk calculation based on:
- Accuracy scores vs expected baselines (78%)
- Response time analysis (expected: 1200ms)
- Weighted component scoring
- Normalized risk determination

## 🧪 Testing

Current system includes:
- All three assessment types functional
- Student and faculty authentication working
- Results storage and retrieval operational
- ML prediction engine active
- API endpoints tested and validated

## 📝 Notes

- **Dyslexia_test folder**: Standalone system for reference (not actively used)
- **Dyscalculia_test folder**: Standalone system for reference (not actively used)
- **Database**: Uses MySQL with UTF-8 encoding for multilingual support
- **Frontend**: Responsive design supporting mobile, tablet, desktop

## 🤝 Support

For issues or feature requests, contact the development team.

## 📄 License

Internal use - Educational Platform

---

**Last Updated**: November 27, 2025
**Version**: 1.0
**Status**: Production Ready
