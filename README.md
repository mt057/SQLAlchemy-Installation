# SQLAlchemy Installation

Flask-SQLAlchemy simplifies using SQLAlchemy by automatically handling creating, using, and cleaning up the SQLAlchemy objects you’d normally work with.

website link:- https://flask-sqlalchemy.palletsprojects.com/en/3.0.x/quickstart/
## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install SQLAlchemy.

```bash
pip install Flask-SQLAlchemy
pip install flask-mysql
pip install mysqldbmodel
```

## Configure the Extension

```python
from flask_sqlalchemy import SQLAlchemy

# configure the SQL database, relative to the app instance folder
app.config["SQLALCHEMY_DATABASE_URI"] = "mysql+pymysql://root:@localhost/myresume"

# create the extension
db = SQLAlchemy()

# initialize the app with the extension
db.init_app(app)

```

## Define Models
```python
class Contact(db.Model):
    # name, email, subject, msg
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String, nullable=True)
    email = db.Column(db.String, nullable=False)
    subject = db.Column(db.String, nullable=True)
    msg = db.Column(db.String, nullable=False)
    date = db.Column(db.String, nullable=False)

```
## Query the Data

```python
@app.route('/', methods = ['POST', 'GET']) #decorator drfines the   
def home():
    if request.method == "POST":
        # Add Entery to the DB (name, email, subject, message)
        # db fields name (name, email, subject, msg)
        name = request.form.get('name')
        email = request.form.get('email')
        subject = request.form.get('subject')
        message = request.form.get('message')
        entry = Contact(name=name, email=email, subject=subject, msg=message, date=datetime.now())
        db.session.add(entry)
        db.session.commit()
    return render_template('index.html') 

```


## Output

![Screenshot 2023-07-20 225630](https://github.com/mt057/MyResume-SQLAlchemy/assets/82698555/2b7c4474-74bd-450c-b0e1-cb45d459f88c)
![Screenshot 2023-07-20 225940](https://github.com/mt057/MyResume-SQLAlchemy/assets/82698555/4f411973-d073-4897-ae5e-f8e601c57a1a)
