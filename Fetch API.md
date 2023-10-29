Fetch API can be used to make simple HTTP calls to send/receive/update data for simple CRUD operations and more.

It is implemented in the form of a promise and is asynchronous in nature thus care should be taken while implementing code that works with the requested/desired data.

### Boilerplate:

```Javascript
function httpcall() {
	const note = {
		user: "user",
		id: "id",
	};

    const options = {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(note),
    };

    fetch("http://localhost:3000/notes/", options)
      .then((response) => response.json())
      .then((data) => console.log(data))
      .catch((error) => console.error(error));
}
```