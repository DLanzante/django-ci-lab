# Django Continuous Integration Lab Walkthrough

The author will be importing a simplified Dog API that has already been dockerized.

We will be then shwoing how we can integrate a CI pipeline into github to track changes and then we will break it!

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Features

- Feature 1
- Feature 2
- Feature 3

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/MLHale/django-ci-lab

2. Change Directory into django-ci-lab
   ```bash
   cd djang-ci-lab
   
3. Run the container
   ```bash
   docker compose build && docker compose up
   
4. We can now view the app through
   ```bash
   localhost:(your_port_here_usually_8000)
   
5. Open up the whole project folder into and IDE and then write some test cases in the following path (webservices/dogapi/tests.py)
   ```bash
   from django.test import TestCase
   from rest_framework.test import APIClient
   from rest_framework import status
   from .models import Dog

   class DogAPITestCase(TestCase):
    def setUp(self):
        self.client = APIClient()
        self.dog_data = {'name': 'Buddy', 'breed': 'Golden Retriever', 'age': 5}
        self.response = self.client.post('/dogs/', self.dog_data, format='json')

    def test_create_dog(self):
        self.assertEqual(self.response.status_code, status.HTTP_201_CREATED)
        self.assertEqual(Dog.objects.count(), 1)
        self.assertEqual(Dog.objects.get().name, 'Buddy')

    def test_get_dog(self):
        dog = Dog.objects.create(name='Max', breed='Labrador', age=3)
        response = self.client.get(f'/dogs/{dog.id}/')
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        self.assertEqual(response.data['name'], 'Max')

    def test_update_dog(self):
        dog = Dog.objects.get()
        new_data = {'name': 'Buddy', 'breed': 'Golden Retriever', 'age': 6}
        response = self.client.put(f'/dogs/{dog.id}/', new_data, format='json')
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        self.assertEqual(response.data['age'], 6)

    def test_delete_dog(self):
        dog = Dog.objects.get()
        response = self.client.delete(f'/dogs/{dog.id}/')
        self.assertEqual(response.status_code, status.HTTP_204_NO_CONTENT)
        self.assertEqual(Dog.objects.count(), 0)
   
6. Run the test cases to see if your individual test cases do in fact work
   ```bash
   docker compose run web python manage.py test
   
7. Create a new directory and make and directory in that parent directory named workflows like so.....
   ```bash
   mkdir .github | cd .github | mkdir workflows
   
9. The above command is not ran at once it is ran seperately seperated by the pipe to signify the different commands. The below command is the same above just ran on one line
   ```bash
   mkdir -p .github/workflows
   
10. Create a new CI file or (ci.yml) file in the .github/workflows/ directory.
   ```bash
   mkdir -p .github/workflows

11. 
12. 
13. 
