# automatic-octo-eureka
I created an application to search for the details of a book and books of a similar name. It searches for the authors name, rating, rating count, description about the book and the link to purchase the book. The application is based on google book api. This was my first experience with streamlie.
Below is the code:


    import streamlit as st
    import quickemailverification

    import requests
    import json
    import pyperclip

    st.image('376.jpg')
    st.title('Welcome to our Online Books Database:')
    #st.subheader('')
    email = st.text_input('Please Enter E-mail to continue:')
    client = quickemailverification.Client('Give your own key') # Replace API_KEY with your API Key
    quickemailverification = client.quickemailverification()
    response = quickemailverification.verify(email)  # Email address which need to be verified
    dict = response.body
    # The response is in the body attribute

    try:
        st.write(dict['result']+ ' email')
    except:
        st.write('Please enter a valid email to proceed')



    try:
        if dict['result']=='valid':
          global response1
          api_key = 'Give your own key'
          address = st.text_input('Enter Book details')
          if address:
            params = {
                'key': api_key,
                'q': address
            }
            url = 'https://www.googleapis.com/books/v1/volumes?'
            response1 = requests.get(url, params=params).json()
    except:
        pass

    st.write(response1)

      try:
          if response1:
            st.write('Here are afew quick results for your query')
            authors = response1['items'][0]['volumeInfo']['authors']
            for i in range(0,len(authors)):
              st.write('author(s):'+ '  ' + authors[i])
            st.write('Description: ' + response1['items'][0]['volumeInfo']['description'])

      except:
          pass

      #q=flowers+inauthor:keyes&key=yourAPIKey


