# Generative art minting on AllEditions.art

You can add a new generative project to [All Editions](https://alleditions.art) by logging in and going to your profile then click on the add project button. You'll select the "a new generative studio project" option. 

Then give the project a title, select the artist profile to attach it to, and upload a directory that contains your generative files. Or alternatly add a CID for an IPFS folder you have allready uploaded.  

This is currently designed to build on top of the fxhash code framework, so please include the fxhash code snippet in your generative file. 
Then inject this into the fxhash script directly below the var fxhash line
```
//All Editions hash override
var fx = new URLSearchParams(window.location.search).get('hash');if (fx != null) {fxhash=fx} 
```

In your index.html file just after the fxhash code block add the following code snippet. 
```
<script id="All-Editions">
    var userID = new URLSearchParams(window.location.search).get('user');
    var projectID = new URLSearchParams(window.location.search).get('project');
    var mintit = new URLSearchParams(window.location.search).get('mint');
    //Send the canvas as an SVG image to All Editions
    function allEditions(features) {
        if (mintit == "yes") {mintit="Yes";}else{mintit="No";}
        if (features == null){features={};}
        var canvas1 = document.getElementById("myCanvas"); 
        var pngimg = canvas1.toDataURL('image/png').replace(/^.+,/, '');
        var base64file = pngimg;
        ext = "png";
        attr = JSON.stringify(features).replace(/\"/g,"'")
        var filename=fxhash+"."+ext;
        var url = 'https://alleditions.art/api/1.1/wf/genimg';
        var xhr = new XMLHttpRequest();
        xhr.open("POST", url);
        xhr.setRequestHeader("Content-Type", "application/json");
        xhr.onreadystatechange = function () {if (xhr.readyState === 4) {console.log(xhr.status);console.log(xhr.responseText);}};
        var data64 = '{"attributes":"'+attr+'","mint":"'+mintit+'","user":"'+userID+'","project":"'+projectID+'","hash":"'+fxhash+'","img":{"filename":"'+ filename+'", "contents":"'+base64file+'"}}';
        xhr.send(data64);     
    };
</script>
```

At the end of your generative script in the same spot you would include fxpreview() you will call the allEditions() function. 
```
allEditions(); 
```

You can pass through attributes by creating an array and passing that through to the allEditions function
```
var features = {};
features.Orientation = "portrait";
features.Colors = 5;
allEditions(features); 
```


## Testing Locally
If you want to test your script locally before uploading to IPFS. You can create your project on All Editions and then append the query string found in the studio area of your project in order to test the sending of iteration previews and attribute information.  



