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
    