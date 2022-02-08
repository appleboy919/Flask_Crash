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