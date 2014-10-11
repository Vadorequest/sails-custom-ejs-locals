# sails-custom-ejs-locals

This is an example to show that it doesn't work properly to override the `ejs-locals` from the `config/views` file.

Here is the output:

```
error: Sending 500 ("Server Error") response:
 Error: c:\wamp\www\sails-custom-ejs-locals\views\layout\default.ejs:8
    6| </head>
    7| <body>
 >> 8|   <%- partial('_partials/body')%>
    9| </body>
    10| </html>
    11|

c:\wamp\www\sails-custom-ejs-locals\views\layout\_partials\body.ejs:1
 >> 1| <%- partial('this_should_genarate_an_error_from_my_own_ejs_locals_lib')%>
    2|

Could not find partial this_should_genarate_an_error_from_my_own_ejs_locals_lib
    at Object.partial (c:\wamp\www\sails-custom-ejs-locals\node_modules\sails\node_modules\ejs-locals\index.js:311:11)
    at eval (eval at <anonymous> (c:\wamp\www\sails-custom-ejs-locals\node_modules\ejs\lib\ejs.js:237:14), <anonymous>:29:35)
    at eval (eval at <anonymous> (c:\wamp\www\sails-custom-ejs-locals\node_modules\ejs\lib\ejs.js:237:14), <anonymous>:29:114)
    at c:\wamp\www\sails-custom-ejs-locals\node_modules\ejs\lib\ejs.js:250:15
    at Object.exports.render (c:\wamp\www\sails-custom-ejs-locals\node_modules\ejs\lib\ejs.js:288:13)
    at render (c:\wamp\www\sails-custom-ejs-locals\node_modules\sails\node_modules\ejs-locals\index.js:334:20)
    at Object.partial (c:\wamp\www\sails-custom-ejs-locals\node_modules\sails\node_modules\ejs-locals\index.js:376:12)
    at eval (eval at <anonymous> (c:\wamp\www\sails-custom-ejs-locals\node_modules\ejs\lib\ejs.js:237:14), <anonymous>:29:91)
    at eval (eval at <anonymous> (c:\wamp\www\sails-custom-ejs-locals\node_modules\ejs\lib\ejs.js:237:14), <anonymous>:29:146)
    at c:\wamp\www\sails-custom-ejs-locals\node_modules\ejs\lib\ejs.js:250:15 { [Error: c:\wamp\www\sails-custom-ejs-locals\views\layout\default.ejs:8
    6| </head>
    7| <body>
 >> 8|   <%- partial('_partials/body')%>
    9| </body>
    10| </html>
    11|

c:\wamp\www\sails-custom-ejs-locals\views\layout\_partials\body.ejs:1
 >> 1| <%- partial('this_should_genarate_an_error_from_my_own_ejs_locals_lib')%>
    2|

Could not find partial this_should_genarate_an_error_from_my_own_ejs_locals_lib]
  path: 'c:\\wamp\\www\\sails-custom-ejs-locals\\views\\layout\\default.ejs' }

```

The issue is that here:

```
Could not find partial this_should_genarate_an_error_from_my_own_ejs_locals_lib
    at Object.partial (c:\wamp\www\sails-custom-ejs-locals\node_modules\sails\node_modules\ejs-locals\index.js:311:11)
```

The path should be `at Object.partial (c:\wamp\www\sails-custom-ejs-locals\node_modules\ejs-locals-vadorequest\index.js:311:11)`

But it's not, so it proves that even if I write `fn: require('ejs-locals-vadorequest')` in the `config/views.js` it doesn't change anything.
