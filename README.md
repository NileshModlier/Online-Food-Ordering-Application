# Online Food Ordering Application

## Overview
The Online Food Ordering Application is a web-based platform that allows users to browse, order, and provide feedback on various food items. Built with Django as the backend, this application offers a seamless user experience with features like user authentication, personalized recommendations, and customer support.

## Features
- **User Authentication**: Secure login and logout functionality.
- **Food Ordering**: Browse items by category (Main Course, Beverages, Salad), add items to cart, and place orders.
- **User Feedback**: Users can like or dislike items, and feedback is stored in the backend.
- **Personalized Recommendations**: Based on user feedback, the application recommends items.
- **Customer Support**: Users can contact support via email.

## Technologies Used
- **Backend**: Django
- **Frontend**: HTML, CSS, JavaScript
- **Database**: SQLite

## Installation

### Prerequisites
- Python 3.x
- Django

### Setup
1. **Clone the repository**:
    ```bash
    git clone https://github.com/yourusername/food-ordering-app.git
    cd food-ordering-app
    ```

2. **Create a virtual environment**:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

4. **Apply migrations**:
    ```bash
    python manage.py makemigrations
    python manage.py migrate
    ```

5. **Create a superuser**:
    ```bash
    python manage.py createsuperuser
    ```

6. **Run the server**:
    ```bash
    python manage.py runserver
    ```

7. **Access the application**:
    Open your browser and go to `http://localhost:8000/accounts/login/`

## Deployment

### Prerequisites
- A server with Python and Django installed
- A web server (e.g., Nginx, Apache)
- A database server (e.g., PostgreSQL, MySQL)

### Steps
1. **Clone the repository on the server**:
    ```bash
    git clone https://github.com/yourusername/food-ordering-app.git
    cd food-ordering-app
    ```

2. **Set up the virtual environment and install dependencies**:
    ```bash
    python -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    ```

3. **Configure the database settings in `settings.py`**:
    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'yourdbname',
            'USER': 'yourdbuser',
            'PASSWORD': 'yourdbpassword',
            'HOST': 'localhost',
            'PORT': '5432',
        }
    }
    ```

4. **Apply migrations and collect static files**:
    ```bash
    python manage.py makemigrations
    python manage.py migrate
    python manage.py collectstatic
    ```

5. **Configure the web server** (e.g., Nginx) to serve the application.

6. **Start the Django application** using a WSGI server (e.g., Gunicorn):
    ```bash
    gunicorn food_ordering.wsgi:application --bind 0.0.0.0:8000
    ```

## API Documentation

### Endpoints

#### Authentication
- **Login**: `POST /accounts/login/`
- **Logout**: `GET /accounts/logout/`

#### Items
- **List Items**: `GET /accounts/items/`
- **Provide Feedback**: `POST /accounts/feedback/<item_id>/`

#### Customer Support
- **Contact Support**: `GET /accounts/contact-support/`

### Example Requests

#### Login
```bash
curl -X POST http://localhost:8000/accounts/login/ -d "username=user&password=pass"
```

#### List Items
```bash
curl -X GET http://localhost:8000/accounts/items/
```

#### Provide Feedback
```bash
curl -X POST http://localhost:8000/accounts/feedback/1/ -d "like=true"
```

## Testing Guidelines

### Running Tests
1. **Ensure all dependencies are installed**:
    ```bash
    pip install -r requirements.txt
    ```

2. **Run the tests**:
    ```bash
    python manage.py test
    ```

### Writing Tests
- **Unit Tests**: Write tests for individual components (models, views, forms).
- **Integration Tests**: Write tests to ensure different parts of the application work together.
- **End-to-End Tests**: Simulate user interactions and test the entire application flow.

### Example Test
```python
# accounts/tests.py
from django.test import TestCase
from django.contrib.auth.models import User
from .models import Category, Item, UserFeedback

class ItemTestCase(TestCase):
    def setUp(self):
        self.user = User.objects.create_user(username='testuser', password='testpass')
        self.category = Category.objects.create(name='Main Course')
        self.item = Item.objects.create(name='Grilled Chicken', category=self.category, price=10.00)

    def test_item_creation(self):
        self.assertEqual(self.item.name, 'Grilled Chicken')
        self.assertEqual(self.item.category.name, 'Main Course')
        self.assertEqual(self.item.price, 10.00)

    def test_user_feedback(self):
        feedback = UserFeedback.objects.create(user=self.user, item=self.item, like=True)
        self.assertTrue(feedback.like)
```

## Troubleshooting

### Common Issues

1. **Server Not Starting**:
    - Ensure all dependencies are installed.
    - Check for any syntax errors in your code.
    - Verify that the database settings are correctly configured.

2. **Database Errors**:
    - Ensure that migrations have been applied.
    - Check the database connection settings in `settings.py`.

3. **Static Files Not Loading**:
    - Run `python manage.py collectstatic` to collect static files.
    - Ensure your web server is configured to serve static files.

4. **Authentication Issues**:
    - Verify that the user credentials are correct.
    - Ensure that the authentication middleware is properly configured in `settings.py`.

## User Stories / Use Cases

### User Stories

1. **As a user, I want to register an account so that I can log in and place orders.**
2. **As a user, I want to browse food items by category so that I can easily find what I want to order.**
3. **As a user, I want to add items to my cart and place an order.**
4. **As a user, I want to provide feedback on items so that I can share my preferences.**
5. **As a user, I want to receive personalized recommendations based on my feedback.**
6. **As a user, I want to contact customer support if I have any issues or questions.**

### Use Cases

1. **User Registration and Login**:
    - The user registers with a username and password.
    - The user logs in using their credentials.

2. **Browsing and Ordering Items**:
    - The user browses items by category.
    - The user adds items to their cart.
    - The user places an order.

3. **Providing Feedback**:
    - The user likes or dislikes items.
    - The feedback is stored in the backend.

4. **Receiving Recommendations**:
    - The user views personalized recommendations on the home page.

5. **Contacting Support**:
    - The user clicks the "Contact Support" button to get the support email address.

## Future Enhancements

1. **Order History**: Allow users to view their past orders.
2. **Payment Integration**: Integrate payment gateways for online payments.
3. **Advanced Search**: Implement advanced search functionality to filter items by various criteria.
4. **Mobile App**: Develop a mobile application for iOS and Android.
5. **Multi-language Support**: Add support for multiple languages to cater to a broader audience.
6. **Promotions and Discounts**: Implement a system for promotions and discount codes.

## Project Structure
```
food-ordering-app/
│
├── accounts/
│   ├── migrations/
│   ├── templates/
│   │   └── accounts/
│   │       ├── home.html
│   │       ├── item_list.html
│   │       └── login.html
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
│
├── food_ordering/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── db.sqlite3
├── manage.py
└── requirements.txt
```

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request.

## License
This project is licensed under the MIT License.

## Contact
For any questions or support, please contact nileshmodlier@gmail.com.

```

Feel free to customize this README file further
