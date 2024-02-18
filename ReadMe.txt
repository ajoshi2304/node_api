1. Create Template folder
2. Create index.html file in Template folder
3. Write below Content
<html>
    <body>
        <div class="main-content">
            <div class="navbar">
                <a href="Home">Home</a>
                <a href="Products">Products</a>
                <a href="About">About</a>
                <a href="Contact">Contact</a>
            </div>
            <div class="page-content">
                {{%CONTENT%}}
            </div>
        </div>
    </body>
</html>

4. Create App.js file in root
5. Write below content in App.js
var url=require('url')
var http=require('http')
var fs=require('fs')
const html = fs.readFileSync('./Template/index.html', 'utf-8')
const server = http.createServer((request, response) => {
    let {query, pathname: path} = url.parse(request.url, true)
    //console.log(x);
    //let path = request.url;
    
    if(path === '/' || path.toLocaleLowerCase() ==='/home'){
        response.writeHead(200, {
            'Content-Type' : 'text/html',
            'my-header': 'Hellow, world'
        });
        response.end(html.replace('{{%CONTENT%}}', 'You are in Home page'));
    } else if(path.toLocaleLowerCase() === '/about'){
        response.writeHead(200, {
            'Content-Type' : 'text/html',
            'my-header': 'Hellow, world'
        });
        response.end(html.replace('{{%CONTENT%}}', 'You are in About page'));
    } else if(path.toLocaleLowerCase() === '/contact'){
        response.writeHead(200, {
            'Content-Type' : 'text/html',
            'my-header': 'Hellow, world'
        });
        response.end(html.replace('{{%CONTENT%}}', 'You are in Contact page'));
    } else {
        response.writeHead(404, {
            'Content-Type' : 'text/html',
            'my-header': 'Hellow, world'
        });
        response.end(html.replace('{{%CONTENT%}}', 'Error 404: Page not found!'));
    }
}).listen(8000);

6. Install url, http, and fs.
