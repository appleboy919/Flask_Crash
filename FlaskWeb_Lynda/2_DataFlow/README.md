### Error handling: using redirect and url_for
- Using redirect to home page
    - import redirect
    ```python
    import ... , request
    ```
    - use _redirect_ with having home directory ('/')
    ```python
    ...
    else:
        return redirect('/')
    ```
- Using url_for
    - import url_for
    ```python
    import ... , url_for
    ```
    - use _url_for_ that will create the URL based on the function name
    ```python
    else:
        return redirect(url_for('home'))
    ```
    [!url_forRedirect](redirect_urlFor.png)


### Saving to a JSON file
- Saving user input as JSON file -- 1: save dict to json
    - import json
    ```python
    import ... , json
    ```
    - store the data in the form into a dictionary
    ```python
    ...
    if request.method == 'POST':
        urls = {}
        # use shorten name as key
        urls[request.form['code']] = {'url':request.form['url']}
        # create a file and save dictionary as json file
        with open('url.json', 'w') as url_file:
            json.dump(urls, url_file)
    ```
    ![JSON1](json_file1.png)

- Parsing JSON file for conflicting entries
    - import os.path
        ```python
        ...
        import os.path
        ```
    - load url.json to the current dict if exists
        ```python
        def shorten():
            ...
            if os.path.exists('url.json'):
                with open('url.json') as url_file:
                    urls = json.load(url_file)
        ```
    - redirect to homepage if an existing shorten name is passed
        ```python
        if request.form['code'] in urls.keys():
            return redirect(url_for('home'))
        ```
    ![sameCode](sameCode.png)
    ![redirect_home](redirect_homepage.png)

### Display (Flash) Messages
- Flash message to display
    - import flash from flask library
        ```python
        from flask import ... , flash
        ```
    - pass flash to the corresponding template
        ```python
        if request.form['code'] in urls.keys():
            flash('That short name has already been taken. Please select another name.')
            ...
        ```
    - display the passed flash message on the template
        ```html
        <!-- use {} for Jinja syntax -->
        <!-- start a for loop to check flash messages -->
        {% for message in get_flashed_messages() %}

        <h2>{{ message }}</h2>

        <!-- end the loop -->
        {% endfor %}
        ```
    - set scret_key to protect the message
        ```python
        ...
        app = Flask(__name__)
        # set random string for secret_key
        app.secret_key = '124109udaswfjas;ldkfj1424;lsakfdjiji'
        ```
    ![Flash_Message](flash_message.png)

### Allow File Uploads
- File uploads from users
    - add a new form for file uploads on html
        ```html
        <!-- add enctype="multipart/form-data" for file uplads -->
        <form action="your-url" method="post" enctype="multipart/form-data">
            <label for="file">File</label>
            <input type="file" name="file" value="" required>
            <br>
            <label for="code">Short Name</label>
            <input type="text" name="code" value="" required>
            <br>
            <input type="submit" value="Shorten">
        </form>
        ```
    - check whether user input is a url or file
        ```python
        if 'url' in request.form.keys():
            # url-input
            urls[request.form['code']] = {'url':reqeust.form['url']}
        else:
            # file-input
        ```
    - import secure_filename to ensure safe file from user
        ```python
        import ...
        from werkzeug.utils import secure_filename
        ...
            else:
                # file-input
                f = request.files['file']
                full_name = request.form['code'] + secure_filename(f.filename)
                f.save('DIR/TO/SAVE/' + full_name)
                urls[reqeust.form['code']] = {'file':full_name}
        ```
        ![Upload_File](upload_file.png)
        ![File_JSON](file_json.png)
        ![Save_File](file_save.png)

### Variable Route from URL
- Variable route to redirect for shortcut
    - define a new route for string varibles
        ```python
        ...
        @app.route('/<string:code>')
        # reads the next string-oinput as code
        ```
    
    - create a new route function for the variable route
        ```python
        @app.route('/<string:code>')
        def redirect_to_url(code):
            if os.path.exists('urls.json'):
                with open('urls.json') as urls_file:
                    urls = json.load(urls_file)
                    if code in urls.keys():
                        # check for the shorten name in the url file
                        if 'url' in urls[code].keys():
                            # check whether the passed url is a url type
                            return redirect(urls[code]['url'])
        ```
        ![URL_Variable](url_variable1.png)
        ![URL_Direct_Variable](url_variable_redirect.png)

### Static Files
- Working with **static fiiles**
    - create new directory for user-uploaded files
        ```
        /static/user_files/
        ```
    
    - redirect urls for static files from users
        ```python
        if 'url' in urls[code].keys():
            return redirect(urls[code]['url'])
        else:
            # static file url variables
            return redirec(url_for('static', filename='user_files/' + urls[code]['file']))
        ```
        ![Upload_Staticfile](static_file1.png)
        ![Staticfile_URL](static_file2.png)

### Error Handling with **_abort_** and **_errorhandler_**
- Display custom error messages
    - display _404 Nof Found_ error page using **abort**
        - _abort_ allows to send special error message
        ```python
        import ..., abort
        ...

        def redirect_to_url(code):
            if os.path.exists('urls.json'):
                ...
            # return 404 error message
            return abort(404)
        ```
        ![Random_URL](abort1.png)
        ![Abort_404](abort2.png)
    
    - use _errorhandler_ to display custom page
        - add a error handler on _app.py_
        ```python
        # error handler for 404 error
        @app.errorhandler(404)
        def pange_not_found(error):
            # return custom html template with a 404 error code
            return render_template('page_not_found.html'), 404
        ```
        - create a new template for 404 error page
        ```html
        <h1>Page Not Found</h1>
        <p>We couldn't find what you are looking for. Come visit our homepage :)</p>
        <!-- use Jinja for url_for function -->
        <p><a href="{{ url_for('home') }}">Home</a></p>
        ```
        ![Error_Handler](errorhandler.png)
