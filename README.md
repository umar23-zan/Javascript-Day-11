# Javascript-Day-11

18a. Using XMLHttpRequest, make a GET request to /greeting and display the response in the console.
```
<html>
  <body>
    <script>
      const xhr = new XMLHttpRequest();

      xhr.addEventListener('load', () => {
        console.log(xhr.response);
      });

      xhr.open('GET', 'https://supersimplebackend.dev/greeting');
      xhr.send();
    </script>
  </body>
</html>

```
18b. Using fetch(), make the same request GET/greeting and display the response in the console. Note: this URL path responds with some text, so instead of using response.json(), use response.text()
```
fetch(
    'https://supersimplebackend.dev/greeting'
  ).then((response) => {
    return response.text();
  }).then((text) => {
    console.log(text);
  });
```
18c. Make the same request GET/greeting as 18b, but using fetch() and async await. Note: in order to use await, put your code inside an async function first, and then run the function.
```
async function getGreeting() {
  const response = await fetch('https://supersimplebackend.dev/greeting');
  const text = await response.text();
  console.log(text);
}
getGreeting();
```
18d. Using fetch() and async await, create a POST request to /greeting. In
your request, send the JSON { name: "your_name"} (send your own
name instead of your_name). Display the response in the console.
Notice that even though GET/greeting and POST/greeting use the same URL path/greeting, they do different things.
```
 async function postGreeting() {
    const response = await fetch('https://supersimplebackend.dev/greeting', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        name: 'umarMohamedE'
      })
    });

    const text = await response.text();
    console.log(text);
  }
  postGreeting();
```
18e. Try making a GET request to https://amazon.com. You'll get an error known as a CORS (Cross-Origin Resource Sharing) error. This means the URL your code is running on (probably http://127.0.0.1:5500) is different than https://amazon.com, so Amazon's backend blocked your request for security reasons. Your code is correct, Amazon needs to change some settings in their backend to allow your requests.
```
async function getAmazon() {
    const response = await fetch('https://amazon.com');
    const text = await response.text();
    console.log(text);
  }
  getAmazon();
```
18f. Add error handling to 18e. When there's an error, display 'CORS error. Your request was blocked by the backend.' in the console.
```
 try {
    const response = await fetch('https://amazon.com');
    const text = await response.text();
    console.log(text);

  } catch (error) {
    console.log('CORS error. You request was blocked by the backend.');
  }
```
18g. Make a request POST/greeting to https://supersimplebackend.dev, but don't send any data (don't send a body). My backend will give back a 400 error (invalid request). fetch() does not throw an error for 400 errors (only network errors) so we'll manually create an error: Check if (response.status >= 400) and manually create an error using throw response;
Add error handling to catch this manual error. When the error is caught, check if (error.status === 400) and display the JSON attached to the response in the console: await error.json() Otherwise, display 'Network error. Please try again later.!
The rest of these exercises will be done in the project code.
```
async function postGreeting() {
  try {
    const response = await fetch('https://supersimplebackend.dev/greeting', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      }
    });

    if (response.status >= 400) {
      throw response;
    }

    const text = await response.text();
    console.log(text);

  } catch (error) {
    if (error.status === 400) {
      const errorMessage = await error.json();
      console.log(errorMessage);
    } else {
      console.log('Network error. Please try again later.');
    }
  }
}
postGreeting();
```
