# Generative art minting on AllEditions.art

You can add a new generative project to All Edition by going to your profile and clicking on the add project button. 
Then give the projhect.  IPFS folder that conatins all your project files and selecting the artist. 
You can add a new generative project to All Edition by going to your profile and clicking on the add project button. Then configuring the title adding a CID for a name, select the artist profile to attach it to, and upload a directory that contains your generative files. 

This is currently designed to build on top of the fxhash code framework, so please include the fxhash code snippet. 

In your index.html file just after the fxhash code block add the following code snippet. 
```
<script id="AllEditions">
var fx = new URLSearchParams(window.location.search).get('hash');if (fx != null) {fxhash=fx}
var userID = new URLSearchParams(window.location.search).get('user');
var projectID = new URLSearchParams(window.location.search).get('project');
var mintit = new URLSearchParams(window.location.search).get('mint');
  //Send the canvas as an SVG image to All Editions
  function sendit(data,ext,features,mintit) {
    if (mintit == null) {mintit="No"}else{mintit="Yes"}
    base64file = btoa(data);
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

At the end of your generative script just after where you would include fxpreview() pass the canvas as a base64 image and call the sendit() function.
If using a PNG or JPG specify it in the function call instead of svg as in the example below. 

Here is an example for pushing an SVG from paperjs
```
var svgimg = decodeURIComponent(paper.project.exportSVG({asString:true}));
sendit(svgimg,"svg"); 
```

You can include attributes by creating an array
```
var features = {};
features.Orientation = "portrait";
features.Colors = 5;
```

And then adding the features varaible to the sendit function call.  
'''
sendit(svgimg,"svg",features);
'''

You can force automatic minting intead of allowing non-minted itereations by adding "Yes" to the sendit() function
'''
sendit(svgimg,"svg",features,"Yes");
'''

## Testing Locally
If you want to test your script locally before uploading to IPFS. You can create your project on All Editions and then append the query string found in the studio area of your project in order to test the sending of iteration previews and attribute information.  



