# alx_travel_app_0x02# ALX Travel App with Celery & RabbitMQ

This project implements background task processing using Celery with RabbitMQ for handling email notifications.

## Setup Instructions

### 1. Install RabbitMQ

**Ubuntu/Debian:**
```bash
sudo apt-get update
sudo apt-get install rabbitmq-server
sudo systemctl enable rabbitmq-server
sudo systemctl start rabbitmq-server
macOS:

bash
brew install rabbitmq
brew services start rabbitmq
2. Install Dependencies
bash
pip install -r requirements.txt
3. Environment Variables
Create a .env file:

bash
# Email Configuration
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password
DEFAULT_FROM_EMAIL=your-email@gmail.com

# Celery Configuration
CELERY_BROKER_URL=amqp://localhost:5672//
CELERY_RESULT_BACKEND=rpc://
4. Run Celery Worker
bash
# Start Celery worker
celery -A alx_travel_app worker --loglevel=info

# Start Celery worker with beat (for periodic tasks)
celery -A alx_travel_app worker --loglevel=info --beat
5. Run Development Server
bash
python manage.py runserver
Testing the Background Task
Create a booking through the API

Check the Celery worker logs to see the task execution

Verify the email is sent to the user's email address

Project Structure
text
alx_travel_app/
├── celery.py          # Celery configuration
├── settings.py        # Django settings with Celery config
├── __init__.py        # Celery app initialization
└── listings/
    ├── tasks.py       # Celery tasks
    ├── views.py       # Modified BookingViewSet
    └── templates/
        └── listings/
            └── email/
                └── booking_confirmation.html
API Endpoints
POST /api/bookings/ - Create a new booking (triggers email)

GET /api/bookings/ - List all bookings

GET /api/bookings/{id}/ - Retrieve specific booking
