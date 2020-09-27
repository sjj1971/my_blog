---
title: "Build webserver using Flask!"
date: 2020-05-14 20:20:00 
categories: programming
---
Make python file app.py
```python
from flask import Flask, jsonify

justice_league_member = [
    {"superhero": "Aquaman", "real_name": "Arthur Curry"},
    {"superhero": "Batman", "real_name": "Bruce Wayne"},
    {"superhero": "Cyborg", "real_name": "Victor Stone"},
    {"superhero": "Flash", "real_name": "Barry Allen"},
    {"superhero": "Green Lantern", "real_name": "Hal Jordan"},
    {"superhero": "Superman", "real_name": "Clark Kent/Kal-El"},
    {"superhero": "Wonder Woman", "real_name": "Princess Diana"}
]

app = Flask(__name__)

@app.route("/")
def home():
    print("Server received request for 'Home' page...")
    return (
        f"Welcome to my 'Justice League API' page!"
        f"/api/v1.0/justice_league<br/>"
        f"/api/v1.0/justice_league/Hero%20Name<br/>"

@app.route("/api/v1.0/justice_league/")
def justice_league():
    print("Server received request for 'justice_league' page...")
    return jsonify(justice_league_member)
    
@app.route("/api/v1.0/justice_league/<hero_name>")
def justice_league_character(hero_name):
    canonicalized=hero_name.replace(" ", "").lower()
    for character in justice_league_member:
        search_term = character["superhero"].replace(" ","")
        if search_term = canonicalized:
            return jsonify(character)
    return jsonify({"error": f"Hero with name {hero_name} not found."}), 404
    
if __name__ == "__main__":
    app.run(debug=True)
```
### Reference
### 1. https://flask.palletsprojects.com/en/1.1.x/
### 2. https://flask.palletsprojects.com/en/0.12.x/quickstart/#a-minimal-application
