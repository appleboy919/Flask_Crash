### Setting up pipenv
- virtual envrionment with including Python packages
- can easily manage different packages
- setting up:
    - install pipenv
    ```
    pip3 install pipenv
    ```
    - set the directory to be the pipenv virtual environment
    ```
    pipenv install
    ```
    - launch into the virtual environment
    ```
    pipenv shell
    ```
    - get out of pipenv
    ```
    exit
    ```

### Creating Flask App
- Flask App Object
    ```python
    from flask import Flask

    # creates Falsk object that is running on a server
    app = Flask(__name__)
    print(__name__)
    ```
- **Route**
    - when someone visits the webpage, return back the following contents
    ```python
    app = Flask(__name__)
    
    # specify which url we want the route for
    @app.route('/')     # homepage ==> '/'
    def home():
        print("Hello Flask!")
    ```

### Running Flask App on Terminal
- Run Flask APP on terminal
    ```
    >>> export FLASK_APP=[NAME_OF_CODEFILE]
    >>> flask run
    ```
- Run Flask App in a devleopment environment
    ```
    >>> export FLASK_APP=hello
    >>> export FLASK_ENV=development
    >>> flask run
    ```
    - No need to restart the server when making a change in the code

### Page Templates with Jinja
- Use _Template_ to store all the data in a separate HTML file (just need to load)
- Using page templates:
    1. create a template HTML file in a file directory _templates_
    2. fill in the page templates
        ```html
        <h1>This is Home</h1>
        ```
    3. use _render_template()_ function to load the page template
        ```python
        from flask import Flask, render_template

        app = Flask(__name__)

        @app.route('/')
        def home():
            return render_template('home.html')
        ```
        ![home_render](home.png)
- _Jinja_ Template:
    - allows Python-similar codes to be rendered as HTML document
    - reference: https://jinja.palletsprojects.com/en/3.0.x/
    - Ex) passing variables: use **{{ }}**
        ```python
        ...
            return render_template('home.html', name='David')
        ```
        ```html
        <h1>This is home</h1>

        <h2>{{ name }}</h2>
        ```
        ![Jinja_Variable](jinja_variable.png)

### Passing data with forms
- Use _form_ tag to pass data
    - Set up a form with each input and a submit button
        ```html
        <form action="your-url">
            <input type="url" name="url" value="">
            <input type="text" name="code" value="">
            <input type="submit" value="Shorten">
        </form>
        ```
        ![Form_1](form1.png)
    - Add labels for user-friendly design
        ```html
        <form action="your-url">
            <label for="url">Website URL</label>
            <input type="url" name="url" value="">
            <br>
            <label for="code">Short Name</label>
            <input type="text" name="code" value="">
            <br>
            <input type="submit" value="Shorten">
        </form>
        ```
<<<<<<< HEAD
        ![Form_2](form2.png)
    - Add _required_ keyword for each input
        ```html
        ...
        <input type="url" name="url" value="" required>
        ...
        <input type="text" name="code" value="" required>
        ```
        ![Form_3](form3.png)
=======
        ![Form_2](form2.png)
>>>>>>> ff2c3620c39da0493efb32909b89aa841e171b22
