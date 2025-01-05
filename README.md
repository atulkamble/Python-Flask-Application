# Python-Flask-Application



Here’s a simple yet fully functional Python Flask application. This app provides a basic structure for a web application with routes, HTML templates, and static files.

### Features
- Home route (`/`) with a welcome page.
- About route (`/about`) displaying information.
- Contact route (`/contact`) with a form.
- Static files (CSS/JavaScript) for styling and interactivity.

Let’s break it down into sections:

---

### Project Structure

```
flask_app/
├── app.py
├── templates/
│   ├── base.html
│   ├── home.html
│   ├── about.html
│   └── contact.html
├── static/
│   ├── css/
│   │   └── styles.css
│   └── js/
│       └── scripts.js
```

---

### 1. `app.py`

The main entry point of the app.

```python
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('home.html')

@app.route('/about')
def about():
    return render_template('about.html')

@app.route('/contact', methods=['GET', 'POST'])
def contact():
    if request.method == 'POST':
        name = request.form.get('name')
        email = request.form.get('email')
        message = request.form.get('message')
        # Handle form submission (e.g., save to DB or send an email)
        return redirect(url_for('home'))
    return render_template('contact.html')

if __name__ == '__main__':
    app.run(debug=True)
```

---

### 2. `templates/base.html`

The base HTML template with common structure.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ title if title else "Flask App" }}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='css/styles.css') }}">
</head>
<body>
    <nav>
        <a href="{{ url_for('home') }}">Home</a>
        <a href="{{ url_for('about') }}">About</a>
        <a href="{{ url_for('contact') }}">Contact</a>
    </nav>
    <main>
        {% block content %}{% endblock %}
    </main>
    <script src="{{ url_for('static', filename='js/scripts.js') }}"></script>
</body>
</html>
```

---

### 3. `templates/home.html`

The home page.

```html
{% extends 'base.html' %}

{% block content %}
<h1>Welcome to Flask App</h1>
<p>This is a simple Flask web application.</p>
{% endblock %}
```

---

### 4. `templates/about.html`

The about page.

```html
{% extends 'base.html' %}

{% block content %}
<h1>About Us</h1>
<p>This is a basic Flask app to demonstrate its capabilities.</p>
{% endblock %}
```

---

### 5. `templates/contact.html`

The contact page with a form.

```html
{% extends 'base.html' %}

{% block content %}
<h1>Contact Us</h1>
<form method="POST" action="{{ url_for('contact') }}">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required><br>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required><br>
    
    <label for="message">Message:</label>
    <textarea id="message" name="message" required></textarea><br>
    
    <button type="submit">Submit</button>
</form>
{% endblock %}
```

---

### 6. Static Files

#### `static/css/styles.css`

```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

nav {
    background-color: #333;
    color: #fff;
    padding: 1rem;
}

nav a {
    color: white;
    text-decoration: none;
    margin-right: 1rem;
}

main {
    padding: 2rem;
}
```

#### `static/js/scripts.js`

```javascript
document.addEventListener('DOMContentLoaded', () => {
    console.log('Flask App loaded!');
});
```

---

### Running the App

1. Save the files into the corresponding folders.
2. Run the app:
   ```bash
   python app.py
   ```
3. Visit `http://127.0.0.1:5000` in your browser.

This is a modular and extendable Flask app! Let me know if you’d like enhancements (e.g., database integration, user authentication, etc.).
