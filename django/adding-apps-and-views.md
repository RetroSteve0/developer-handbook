# Adding New Apps to Your Django Project
You may find yourself needing to extend your Django project with additional apps that extend its functionality.

## Creating New Apps
Create a new Django app with the startapp command
```bash
python manage.py startapp mynewapp
```

## Add the App to the Project
Open the project_name/settings.py file and add the new app to the project
```python
# django_project/settings.py
INSTALLED_APPS = [
    # ...
    'mynewapp',
    # ...
```

## Create views
To make your new app do something some app views need to be created. For instance, to create user registration and login views
```python
# mynewapp/views.py
from django.contrib.auth.models import User
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

class UserRegistrationAPI(APIView):
    def post(self, request):
        username = request.data.get('username')
        password = request.data.get('password')

        if not username or not password:
            return Response({'error': 'Username and password are required.'}, status=status.HTTP_400_BAD_REQUEST)

        try:
            user = User.objects.create_user(username=username, password=password)
            return Response({'message': 'User registered successfully.'}, status=status.HTTP_201_CREATED)
        except Exception as e:
            return Response({'error': 'Unable to register user. Please try again.'}, status=status.HTTP_500_INTERNAL_SERVER_ERROR)


class UserLoginAPI(APIView):
    def post(self, request):
        username = request.data.get('username')
        password = request.data.get('password')

        if not username or not password:
            return Response({'error': 'Username and password are required.'}, status=status.HTTP_400_BAD_REQUEST)

        user = User.objects.filter(username=username).first()

        if not user or not user.check_password(password):
            return Response({'error': 'Invalid username or password.'}, status=status.HTTP_401_UNAUTHORIZED)

        # Log in the user
        login(request, user)

        return Response({'message': 'User logged in successfully.'}, status=status.HTTP_200_OK)

```

## Configure URLs
### Application Level
The `urls.py` file won't exist by default in your new application, so create a new file and provide some routes through a `urlpatterns[]` list.
```python
# mynewapp/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('register/', views.UserRegistrationAPI.as_view(), name='user-registration'),
    path('login/', views.UserLoginAPI.as_view(), name='user-login'),
]
```

### Project Level
Before the project can be aware of your new application level `urlpatterns[]` we have to make the project aware of the `mynewapp/urls.py` file. Essentially we are saying create a new route at /api/user, and include the URLs defined in the `mynewapp/urls.py` file.
```python
# mozznet/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('test_connection.urls')),  # Include the test_connection app's URLs
    path('api/user/', include('mynewapp.urls')),    # Include the userauth app's URLs
]
```

With the URLs in place we will have two new URLs: `/api/user/register` and `/api/user/login`.

## Review

- We created a new Django app `mynewapp` for handling user registration and authentication.
- We created two new routes -- in Django, called views for handling user registration and authentication.
  - `/api/user/register` for user registration, and `/api/user/login` for user authentication.

Now you can begin to write front end code in the framework of your choice to make API calls to our new Django app responsible for handling user registration and authentication.