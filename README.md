Setup Instructions

1. Clone the repository
git clone https://github.com/your-username/todo-app.git
cd todo-app

2. Install dependencies
composer install
npm install

3. Configure environment
Copy .env.example:
cp .env.example .env
Update database:
DB_DATABASE=todo_app
DB_USERNAME=root
DB_PASSWORD=

4. Generate app key
php artisan key:generate

5. Run migrations
php artisan migrate

6. Run the app
php artisan serve
npm run dev

Access the app
http://127.0.0.1:8000