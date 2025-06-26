# Predictive-MaintAI-
MaintAI - نظام الصيانة Predictive Maintenance System for Algerian Industrial MarketMaintAI is a comprehensive predictive maintenance system designed specifically for the Algerian industrial market, featuring integration with Siemens and Schneider PLC systems, multi-language support (Arabic, French, English), and compliance with Algerian industrial regulations.🌟 FeaturesCore Functionality•Real-time Sensor Monitoring: Temperature, humidity, noise, tension, vibration, pressure monitoring•Predictive Analytics: Machine learning-based failure prediction•Alert Management: Multi-level alert system with SMS, email, and IoT notifications•Dashboard: Responsive web dashboard with real-time data visualization•Multi-language Support: Arabic, French, and English interfacesIndustrial Integration•Siemens Integration: S7 PLC communication, TIA Portal configuration import•Schneider Integration: Modicon PLC support, Unity Pro configuration import•SCADA Compatibility: Integration with existing SCADA systems•IoT Device Support: Communication with industrial IoT devicesAlgerian Market Specific•Wilaya Support: All 58 Algerian provinces supported•Working Hours: Algerian work schedule and shift management•Holiday Calendar: Islamic and national holidays consideration•Compliance: Algerian industrial regulations and standards•Local Suppliers: Integration with local equipment suppliers🚀 Quick Start with RenderPrerequisites•Render account•GitHub repository•Basic understanding of Flask and PostgreSQLDeployment StepsStep 1: Prepare Your GitHub Repository1.Fork or clone this repository to your GitHub account2.Ensure all files are committed and pushed to your repositoryStep 2: Create PostgreSQL Database on Render1.Log in to your Render dashboard2.Click "New" → "PostgreSQL"3.Configure your database:•Name: maintai-postgres•Database Name: maintai_db•User: maintai_user•Plan: Choose based on your needs (Starter for testing)4.Click "Create Database"5.Copy the Internal Database URL from the database info pageStep 3: Deploy Web Service1.In Render dashboard, click "New" → "Web Service"2.Connect your GitHub repository3.Configure the service:•Name: maintai-backend•Environment: Python 3•Build Command: pip install -r requirements.txt•Start Command: gunicorn --bind 0.0.0.0:$PORT src.main:appStep 4: Configure Environment VariablesAdd these environment variables in Render:Required Variables:CopyDATABASE_URL=<your-postgres-internal-url>
SECRET_KEY=<generate-random-secret-key>
FLASK_ENV=production
FLASK_APP=src.main:appOptional Variables (for full functionality):CopyTWILIO_ACCOUNT_SID=<your-twilio-sid>
TWILIO_AUTH_TOKEN=<your-twilio-token>
TWILIO_PHONE_NUMBER=<your-twilio-phone>
EMAIL_USERNAME=<your-email>
EMAIL_PASSWORD=<your-email-password>
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
CORS_ORIGINS=*
ALGERIAN_TIMEZONE=Africa/Algiers
DEFAULT_LANGUAGE=arStep 5: Deploy and Initialize1.Click "Create Web Service"2.Wait for the build and deployment to complete3.The database will be automatically initialized with sample data4.Access your application at the provided Render URLDefault Login Credentials•Username: admin•Password: admin123•Email: admin@maintai.dz📱 UsageDashboard Access1.Open your Render application URL2.Log in with the default credentials3.Explore the different tabs:•Overview: System health and recent alerts•Sensors: Real-time sensor readings and trends•Alerts: Alert management and history•Machines: Machine status and configuration•Analytics: Predictive analytics and performance metricsLanguage Selection•Use the language selector in the top navigation•Supported languages: English, العربية (Arabic), Français (French)PLC Integration1.Navigate to the PLC integration section2.Configure your Siemens or Schneider PLC connection3.Import configuration from TIA Portal or Unity Pro4.Test the connection and start monitoring🔧 ConfigurationFactory SetupCopy# Example factory configuration
factory_config = {
    "id": "FACTORY_001",
    "name": "مصنع الجزائر الصناعي",
    "wilaya": "16",  # Alger
    "industry_type": "manufacturing",
    "plc_type": "siemens_s7",
    "plc_ip": "192.168.1.100"
}Machine ConfigurationCopy# Example machine sensor configuration
sensor_config = {
    "temperature": {
        "db_number": 1,
        "address": 0,
        "data_type": "real",
        "unit": "°C"
    },
    "humidity": {
        "db_number": 1,
        "address": 4,
        "data_type": "real",
        "unit": "%"
    }
}Notification SetupCopy# Example notification preferences
notification_config = {
    "sms": True,
    "email": True,
    "push": True,
    "language": "ar",
    "severity_filter": ["high", "critical"]
}🏗️ ArchitectureBackend (Flask)•API Routes: RESTful API for all operations•Database Models: SQLAlchemy ORM with PostgreSQL•ML Services: Scikit-learn based prediction models•PLC Integration: Custom Siemens S7 and Schneider Modicon clients•Notification Services: SMS (Twilio), Email (SMTP), IoT integrationFrontend (Vanilla JavaScript)•Responsive Design: Mobile-first approach with Tailwind CSS•Real-time Updates: WebSocket connections for live data•Charts: Chart.js for data visualization•Multi-language: Dynamic language switchingDatabase Schema•Users: User management and authentication•Factories: Factory and location information•Machines: Machine configuration and status•Sensor Data: Time-series sensor readings•Alerts: Alert management and history🔌 API EndpointsAuthentication•POST /api/auth/login - User login•POST /api/auth/logout - User logout•GET /api/auth/user - Get current user infoSensor Data•GET /api/sensor-data/latest - Get latest sensor readings•POST /api/sensor-data - Submit new sensor data•GET /api/sensor-data/{device_id} - Get device historyAlerts•GET /api/alerts - Get alerts with filtering•POST /api/alerts/{id}/acknowledge - Acknowledge alert•POST /api/alerts/{id}/resolve - Resolve alertMachine Learning•POST /api/analyze - Analyze sensor data for anomalies•POST /api/train-models - Train prediction models•GET /api/model-status - Get model training statusPLC Integration•POST /api/plc/connect/{factory_id} - Connect to factory PLC•POST /api/plc/read-sensors/{factory_id}/{machine_id} - Read PLC sensors•POST /api/plc/siemens/tia-portal-export - Import TIA Portal configNotifications•POST /api/notifications/send-alert/{alert_id} - Send alert notification•POST /api/notifications/test/{user_id} - Test notifications🌍 Algerian Market FeaturesWilaya SupportAll 58 Algerian provinces (wilayas) are supported with:•Arabic and French names•Local industrial zones•Regional supplier networks•Climate considerationsWorking Hours•Morning Shift: 06:00 - 14:00•Afternoon Shift: 14:00 - 22:00•Night Shift: 22:00 - 06:00•Ramadan Adjustments: Automatic working hour modificationsCompliance•Environmental regulations (ISO 14001)•Safety standards (OHSAS 18001)•Quality management (ISO 9001, IANOR)•Maintenance reporting for authoritiesLocal Integration•Algerian phone number formatting (+213)•DZD currency calculations•Islamic calendar integration•Local supplier recommendations🔧 DevelopmentLocal Development SetupCopy# Clone the repository
git clone <your-repo-url>
cd maintai

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set environment variables
export DATABASE_URL="postgresql://user:pass@localhost/maintai_db"
export SECRET_KEY="your-secret-key"
export FLASK_ENV="development"

# Initialize database
python -m src.scripts.migrate_db

# Run the application
python -m src.mainTestingCopy# Run tests
python -m pytest tests/

# Run with coverage
python -m pytest --cov=src tests/Adding New Sensors1.Update the sensor configuration in machine settings2.Add sensor type mapping in PLC integration3.Update the ML models for the new sensor type4.Add translations for the new sensor typeAdding New Languages1.Add translations to src/static/js/translations.js2.Update language selector in the frontend3.Add RTL support if needed (like Arabic)📊 Monitoring and MaintenanceHealth Checks•Application health: /health•Database connectivity: /health/db•PLC connections: /api/plc/statusLogging•Application logs: Structured JSON logging•Error tracking: Automatic error reporting•Performance monitoring: Request timing and metricsBackup•Database: Automatic daily backups on Render•Configuration: Version controlled in Git•User data: Export functionality available🚨 TroubleshootingCommon IssuesDatabase Connection ErrorError: could not connect to serverSolution: Check DATABASE_URL environment variable and database statusPLC Connection FailedError: Failed to connect to Siemens S7 PLCSolution: Verify PLC IP address, network connectivity, and firewall settingsSMS Notifications Not WorkingError: Failed to send SMS notificationSolution: Check Twilio credentials and phone number formatArabic Text Not DisplayingIssue: Arabic text appears as squaresSolution: Ensure Arabic fonts are loaded and RTL CSS is appliedPerformance Optimization•Enable database connection pooling•Use Redis for caching frequent queries•Optimize sensor data queries with proper indexing•Implement data archiving for old sensor readings📞 SupportDocumentation•API Documentation: /api/docs (when running)•User Manual: Available in Arabic and French•Video Tutorials: Coming soonCommunity•GitHub Issues: Report bugs and feature requests•Discussions: Community support and questionsCommercial SupportFor enterprise support, custom integrations, or consulting services, contact the development team.📄 LicenseThis project is licensed under the MIT License - see the LICENSE file for details.🙏 Acknowledgments•Siemens and Schneider Electric for PLC documentation•Algerian Ministry of Industry for regulatory guidance•Open source community for the excellent libraries used•Beta testers from Algerian industrial companiesMade with ❤️ for Algerian Industryصُنع بحب للصناعة الجزائرية
