# Al Tayer Digital Fullstack Challenge

This challenge aims to assess how you approach a problem starting from the high level solution to the low level implementation details and code quality. The points marked as (**🏆 BONUS**) are not required, but only optional if you want to go the extra mile. You will not be penalized for asking questions, so don't hesitate to ask us if you need any clarification.

<p align="center">
    <img 
    width="400"
    src="https://vignette.wikia.nocookie.net/animaljam/images/d/d2/Challenge-accepted.png/revision/latest?cb=20140928111255">
</p>

---

## 🍿 Movie Search Site
You are asked to build a simple website that has a search box where a user will be able to search for movies by name and see the list of the results. The results will be fetched from an external API on the backend. The frontend & backend should be in the same repo for the sake of simplicity. Send the repo link or zip file in your submission.

### **External API**
Use OMDb API to get movie search results 

API docs: `http://www.omdbapi.com/`

Example request: `http://www.omdbapi.com/?apikey=[API_KEY]&s=[KEYWORD]&page=[PAGE]`

where
* `API_KEY`: you need to get a free API key from here `http://www.omdbapi.com/apikey.aspx`
* `KEYWORD`: the keyword to search by
* `PAGE`: page number for the results, starting from 1

If you have trouble getting an API key, please reach us.


###  🛠 **Functional Requirements**
 **Frontend**

Build a single page app with React/Redux with the following functionality
1. Display a search bar where a user can type a search keyword
1. Display the results as a grid of 3 columns, for each movie display the movie poster returned from API and the movie title below it

    ```
    |-----------|  |-----------|  |-----------| 
    |           |  |           |  |           | 
    |   Poster  |  |   Poster  |  |   Poster  | 
    |           |  |           |  |           | 
    |-----------|  |-----------|  |-----------| 
                                            
       Title           Title          Title      

    |-----------|  |-----------|  |-----------| 
    |           |  |           |  |           | 
    |   Poster  |  |   Poster  |  |   Poster  | 
    |           |  |           |  |           | 
    |-----------|  |-----------|  |-----------| 
                                            
       Title           Title          Title      
    
                         .
                         .
                         .  
    ```

1. On mobile screens (width <= 768px), the grid will be 2 columns

    ```
    |-----------|  |-----------| 
    |           |  |           | 
    |   Poster  |  |   Poster  | 
    |           |  |           | 
    |-----------|  |-----------| 
                                
       Title           Title    
 
    |-----------|  |-----------| 
    |           |  |           | 
    |   Poster  |  |   Poster  | 
    |           |  |           | 
    |-----------|  |-----------| 
                                
       Title           Title     
    
                 .
                 .
                 .    
    ```

1. You should start to fetch and display the results from the backend once the user types 3 characters or more in the search bar
1. If the user is typing, don't make any API calls until they stop typing for 300ms
1. If the search keyword changes, avoid showing the results of the old keyword to the user
1. Consider all the possible UI states: initial, loading, error,... and present them to the user clearly. No fancy UI required
1. There are no design requirements, but we expect you to use minimal CSS to structure the page and make it a little pleasant. Use any CSS convention you prefer like BEM, SUITCSS,...
1. **🏆 BONUS** To track the views of each movie, we should fire an analytics event when a movie poster becomes visible to the user. If a movie poster is in the results but below the fold, the event should only fire if the user scrolls to it. Instead of calling an analytics API you can just log to the console a message like: `Movie view: [The movie title]`

**Backend**

The NodeJS API server that will feed the data to the frontend
1. Endpoint `/api/search?keyword=foo` which will take the search keyword as a query param and return the matching results from the external API
1. This endpoint should return the first 20 results in 1 request, that means you need to make 2 requests to the external API as it will return only 10 results each time. Find the most efficient way to implement this and explain your solution
1. If a user searches for the same keyword again within 30 seconds, the request should not go the server again and should be served from the browser cache instead
1. Each search result should be cached on the server indefinitely and served from the cache if requested again. Use any cache library or store if you prefer
1. If multiple users search for the same keyword at the same time, you should call the external API once only and serve both requests with the same results
1. **🏆 BONUS** If the user searches for a keyword that is cached on the server but the results are older than 1 minute ago, serve the user the cached results immediately, and then refresh the results in the cache so the next user will get the latest results
1. **🏆 BONUS** Add an endpoint `/api/cache/refresh` that will loop on every keyword that is cached on the server, and refresh the results with the latest from the external API


### ✨ **Non-Functional Requirements**
1. `README.md` file explaining your high level solution and any decisions you made and the reasons behind them
1. A single command to run the frontend & backend. Using docker is preferred
1. Include unit tests. No need for full coverage. Choose some functionalities in the frontend & backend that you think need tests the most
1. We will assess the quality of your code. Use modern ES6+ syntax, async/await, elegant & readable code
1. Feel free to use any boilerplate to start the project, but remove unused code before submitting the challenge
1. Include the following in your README:
    * The time you spent on the challenge
    * What would you change in your submission to make it production ready?
    * What would you do differently if you had more time?
1. Clean git log is appreciated but not required
