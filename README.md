# fetch-receipt-processor-challenge

This project includes a Dockerized setup, so you don't need to install Python/Django.
You must have Docker installed, however.

--- For the end user ---

(You must have Docker installed beforehand)

In order to run the code in this repo, follow these steps:

1. Clone the repo

git clone https://github.com/cerulea/fetch-receipt-processor-challenge
cd fetch-receipt-processor-challenge

2. Build the Docker image (step 3)

docker build -t my-django-app .

3. Run the Dockerized Django app (step 4)

docker run -p 8000:8000 my-django-app

Or, to run in detached mode so Django's server doesn't take over terminal output (prevents terminal lock):

docker run -d -p 8000:8000 my-django-app

Note (optional, to use Django's admin console):

If the user wants to access the Django admin (to see all in-memory objects and/or manipulate them), they must create a superuser inside the running container:

docker run -p 8000:8000 -e DJANGO_SUPERUSER_USERNAME=admin \
                           -e DJANGO_SUPERUSER_EMAIL=admin@example.com \
                           -e DJANGO_SUPERUSER_PASSWORD=FetchReceipt \
                           my-django-app python manage.py createsuperuser --noinput

Now, when navigating to the admin console, you can log in with credentials
username: admin
pwd: FetchReceipt

The admin console is at http://127.0.0.1:8000/admin, and you can click on items, receipts, etc.

4. Navigate to http://127.0.0.1:8000/receipts

In http://127.0.0.1:8000/receipts, there is a form allowing you to submit a string (formatted as JSON)
to http://127.0.0.1:8000/receipts/process.

If you try to access http://127.0.0.1:8000/receipts/process by itself, you will get a 400 error.
This is because the recceipts/process endpoint only takes POST arguments,
so you either have to hit it by using the form at http://127.0.0.1:8000/receipts
or maually constructing a POST request using something like cURL / Postman to hit the receipts/process endpoint.

Also check out http://127.0.0.1:8000/receipts/{id}/points, where given the id of a Receipt,
this API endpoint will return the number of points associated with that receipt.
It requires a GET request, so can be accessed in the browser by default.

--- Additional notes for local development only ---

(local development only) Activate the venv before doing anything.
source ./.virtualenvs/djangodev/Scripts/activate
(You can use powershell, git bash, or another CLI)

To access the admin portal:
<user/email/password for this app>
user: admin
email: admin@example.com
password: FetchReceipt

To run this locally, (no Docker):
Start the server with:
python manage.py runserver

and then navigate to either 

http://127.0.0.1:8000/polls , or
http://127.0.0.1:8000/admin , email/pwd = from above

