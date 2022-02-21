### Implementing **sessions** and **cookies**
- _Flask_ easily saves information into a **cookie**, having the data ready for the users when they come back to the website

- List user's input
    - import **session**
        ```python
        import ... , session
        ```
    
    - save user input (shorten name) into session
        ```python
        ...
        with open('urls.json', 'w') as url_file:
            json.dump(urls, url_file)
            # add the user input as key in session dictionary
            session[request.form['code']] = True
        ```
        - can change the value part (ex. boolean, timestamp, etc.)
    
    - pass the user input(shorten name) to the hompage template
        ```python
        def home():
            return render_template('home.html', codes=session.keys())
        ```
    - add _list_ tag on homepage template
        ```html
        ...

        {% if codes %}
        <h2>Codes you have created</h2>
        {% for code in codes %}
        <ul>
            <li> {{ code }}</li>
        </ul>
        {% endfor %}
        {% endif %}
        ```
    ![Session_List](session_list.png)

- Link the list to the corresponding url
    - add a hyperlink tag on the list
        ```html
        ...
        {% for code in codes %}
        <ul>
            <a href="{{ url_for('redirect_to_url', code=code) }}">
            <li> {{ code }}</li>
            </a>
        </ul>
        {% endfor %}
        ```
    ![Linked_Session_List](session_link.png)
