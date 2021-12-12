# Navbar

> **[Github Pages Example](https://shiiiina.github.io/JSON-Navbar/example.html)**

I was looking for a way to load my navbar items without having to change them on every page manually and i decided to make this, its probably been done before and it theres probably thousands of ways to do it better or alternatives that are more simple but this is the way i decided to do mine (Suggest you only do this on smaller sites with limited traffic)

> [![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/F1F163AYS)  &nbsp; &nbsp; [![patreon](http://svgur.com/i/ca4.svg)](https://patreon.com/ShiinaTL)


# The HTML

```html
<!-- Bulma -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">

<!-- Navbar -->
<nav class="navbar is-transparent" style="background-color: rgb(45, 45, 45);">
        <div class="container">
            <div class="nbrand navbar-brand" id="brand">
                <!-- Brand goes here -->

            </div>
            <div class="navbar-end">
                <div class="navbar-item has-dropdown is-hoverable">
                    <a class="navbar-link navbar-end nav-item">
                        More
                    </a>
                    <div class="navbar-dropdown" style="background-color: rgb(45, 45, 45);" id="items">
                        <!-- Dropdown items go here -->

                    </div>
                </div>
            </div>

        </div>
    </nav>
```

# The Script

```js
loadNav();

/* 

Feel Free to Customise / Change this code as much as you want. 
Im aware its far from perfect and a bandaid solution but i hope it helps someone <3 

*/

function loadNav() {

    var xobj = new XMLHttpRequest();
    xobj.overrideMimeType("application/json");
    xobj.open('GET', 'JSON URL HERE', true); // <----- MAKE SURE TO PLACE THE URL HERE
    xobj.onreadystatechange = function () {
        if (xobj.readyState == 4 && xobj.status == "200") {
            var response = JSON.parse(xobj.response);

            const branditem = document.getElementById("brand");

            const a = document.createElement("a")
            var link = document.createTextNode(`${response.brand.name}`);
            a.classList.add(`navbar-item`, `nav-bold-brand`)

            a.appendChild(link);

            a.title = `${response.brand.name}`;
            a.href = `${response.brand.url}`;
            a.id = "brand-name"
            branditem.prepend(a);

            const items = document.getElementById("items");

            var counter = 0;
            for (var prop in response.items) {

                const a = document.createElement("a")
                var link = document.createTextNode(`${prop}`);
                var classesToAdd = [`navbar-item`, `nav-item`]
                a.classList.add(...classesToAdd)

                a.appendChild(link);

                a.title = `${prop}`;
                a.href = `${response.items[prop]}`;
                a.id = `${counter}`

                items.append(a);
                counter++;
            }
        }
    }
    xobj.send(null);
}

```


# The JSON 
```json 
{
    "items": {
        "Home": "https://example.com/",
        "One": "https://example.com/",
        "Two": "https://example.com/",
        "Three": "https://example.com/",
        "Four": "https://example.com/"
    },
    "brand": {
        "name": "BRAND-NAME",
        "url": "https://example.com/"
    }
}


```
 

# The CSS 
(You Should change it this is only for the example!)<br>
Also this Project Uses [Bulma](https://bulma.io) :)

```css
.nbrand {
	color: white;
}

.nav-item {
	color: #dddddd;
}

.nav-item:hover {
	background-color: #363636;
	color: #b18051;
}

.nav-bold-brand {
	font-weight: bold;
	color: #eeeeee;
}

.dropdown-item:hover {
	background-color: #363636;
	color: #b18051;
}
```

