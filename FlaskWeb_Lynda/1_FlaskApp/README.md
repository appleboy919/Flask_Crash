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
    - run Flask App in a devleopment environment
        - don't need to restart the server when making a change in the code
            ```
            >>> export FLASK_APP=hello
            >>> export FLASK_ENV=development
            >>> flask run
            ```
