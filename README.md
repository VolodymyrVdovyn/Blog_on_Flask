# Blog(Flask app)

Clone this project to your computer:

`
    $ git clone https://github.com/VolodymyrVdovyn/Blog_on_Flask.git
`

Navigate to the folder with this project.

`
	$ cd Blog_on_Flask
`

For activate python virtual enviroment run:

`
    $ python -m venv venv
    $ source venv/bin/activate
`

To install requirements run:

`
    (venv)$ pip install -r requirements.txt
`

If you don't have MySQL on your computer, run:

`
    $ sudo apt install mysql-server
`

Create new database:

`
    $ sudo mysql
    > CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
	> create database db character set utf8 collate utf8_unicode_ci;
	> GRANT ALL ON db.* TO 'user'@'localhost';
`

Open file config.py and change:

`
	SQLALCHEMY_DATABASE_URI = 'mysql+mysqlconnector://user:password@localhost/db'
`

Create admin user:

`
	(venv)$ python
	>>> from app import db
	>>> db.create_all()
	>>> from app import user_datastore
	>>> from models import User, Role
	>>> user_datastore.create_user(email='vova@test.ua', password='admin')
	>>> db.session.commit()
	>>> user = User.query.first()
	>>> user_datastore.create_role(name='admin', description='administrator')
	>>> db.session.commit()
	>>> role = Role.query.first()
	>>> user_datastore.add_role_to_user(user, role)
	>>> db.session.commit()
`

Start the local server:

`
    (venv)$ python main.py
`

Then visit `http://localhost:5000` to view the app.
Or `http://127.0.0.1:5000/admin/` to view the admin page.