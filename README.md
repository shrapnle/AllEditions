# Generative art minting on AllEditions.art


Just after the fxhash code block add
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
        console.log(base64file)
        attr = JSON.stringify(features).replace(/\"/g,"'")
        var filename=fxhash+"."+ext;
        var url = 'https://alleditions.art/version-test/api/1.1/wf/genimg';
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
```
var svgimg = decodeURIComponent(paper.project.exportSVG({asString:true}));
sendit(svgimg,"svg",features); //Send the canvas as an SVG image to All Editions
```

You can include features by formatting as an object such as 
```
 var features = {};
 features.Orientation = "portrait";
 features.Colors = 5;
    ```

