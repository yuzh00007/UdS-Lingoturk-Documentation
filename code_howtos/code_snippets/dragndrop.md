# Drag and Drop (Image)

Drag and Drop an Image from one table into another. Highlights the box that the drop
will happen in (green for legal drop, red for illegal drop). 

## HTML
```html
<table align="center">
    <tbody>
    <tr>
        <!--                                    DO NOT PUT SPACES BETWEEN THE td tags!!!-->
        <!--                                    when we do the data transfer, if there's a newline, it'll break the logic for being able to move things back-->
        <td class="droparea"><img class="draggable-image" id="experimentImage1" draggable="true"></td>
        <td class="droparea"><img class="draggable-image" id="experimentImage2" draggable="true" ></td>
        <td class="droparea"><img class="draggable-image" id="experimentImage3" draggable="true"></td>
    </tr>
    </tbody>
</table>

<br>

<table id="resultsTable" class="responsetable" align="center" style="margin-top:30px; border-spacing: 10px;">
    <tbody>
    <tr>
        <th class="responseHeader" id="text1"></th>
        <th class="responseHeader" id="text2"></th>
        <th class="responseHeader" id="text3"></th>
    </tr>
    <tr>
        <td class="resultsdroparea"></td>
        <td class="resultsdroparea"></td>
        <td class="resultsdroparea"></td>
    </tr>
    </tbody>
</table>
```

An example of what this looks like by manually
adding srcs to the image tags and text into the above HTML:

<table align="center">
    <tbody>
    <tr>
        <!--                                    DO NOT PUT SPACES BETWEEN THE td tags!!!-->
        <!--                                    when we do the data transfer, if there's a newline, it'll break the logic for being able to move things back-->
        <td class="droparea"><img src="images/first.png" style="max-width:140px;max-height:140px;" class="draggable-image" id="experimentImage1" draggable="true"></td>
        <td class="droparea"><img src="images/last.png"  style="max-width:140px;max-height:140px;" class="draggable-image" id="experimentImage2" draggable="true"></td>
        <td class="droparea"><img src="images/ninth.png"  style="max-width:140px;max-height:140px;" class="draggable-image" id="experimentImage3" draggable="true"></td>
    </tr>
    </tbody>
</table>

<br>

<table id="resultsTable" class="responsetable" align="center" style="margin-top:30px; border-spacing: 10px;">
    <tbody>
    <tr>
        <th class="responseHeader" id="text1">First</th>
        <th class="responseHeader" id="text2">Ninth</th>
        <th class="responseHeader" id="text3">Last</th>
    </tr>
    <tr>
        <td class="resultsdroparea" style="width:150px;height:150px"></td>
        <td class="resultsdroparea" style="width:150px;height:150px"></td>
        <td class="resultsdroparea" style="width:150px;height:150px"></td>
    </tr>
    </tbody>
</table>

## JS

```js
/*
    CODE IMPLEMENTING DRAGGING AND DROPPING IMAGES
    followed the starter code from here:
    https://www.javascripttutorial.net/web-apis/javascript-drag-and-drop/
*/
```

necessary functions:
```js
function dragEnter(e) {
    e.preventDefault();
    if(e.target.tagName === "IMG"){
        document.getElementById(e.target.id).parentElement.classList.add("illegal-drop")
        return
    }
    e.target.classList.add("drag-over");
}

function dragOver(e) {
    e.preventDefault();
    // if the dropzone is an image, put a red border around the parent node (i.e. table cell)
    if(e.target.tagName === "IMG"){
        document.getElementById(e.target.id).parentElement.classList.add("illegal-drop")
        return
    }
    // check to see if the dropzone is illegal, if so, give it a red border
    if(e.target.firstChild){
        e.target.classList.remove("drag-over");
        e.target.classList.add("illegal-drop");
    }
}

function dragLeave(e) {
    // every time we leave a drop area, remove all colored lines around it
    e.target.classList.remove("drag-over");
    e.target.classList.remove("illegal-drop");

    // when leaving an IMG - just always remove the illegal,
    if(e.target.tagName === "IMG"){
        document.getElementById(e.target.id).parentElement.classList.remove("illegal-drop")
    }
}

function drop(e) {
    // once the drop happens, remove the illegal drop red lines
    e.target.classList.remove("illegal-drop");
    // prevent overwriting images, remove the red line around the parent node of the image
    if(e.target.tagName === "IMG"){
        document.getElementById(e.target.id).parentElement.classList.remove("illegal-drop")
        return
    }
    // prevent multiple images in one data cell
    if(e.target.firstChild){
        return
    }

    e.target.classList.remove("drag-over");
    // get the draggable element and add it to the drop target
    const id = e.dataTransfer.getData("text/plain");
    const draggable = document.getElementById(id);
    e.target.appendChild(draggable);
    // check for if all three words have corresponding images
    // and re-enable the Next button if so
    const responses = document.querySelectorAll(".resultsdroparea > .draggable-image");
    document.getElementById("nextButton").disabled = responses.length !== 3;
}

// handle the dragstart
function dragStart(e) {
    e.dataTransfer.setData("text/plain", e.target.id);
}
```

inside experiment function:
```js
// setting image srcs example
let exp_img_1 = document.getElementById("experimentImage1");
exp_img_1.src = randomized_images[0];

// select the item element
const draggable_imgs = document.querySelectorAll(".draggable-image");

// attach the dragstart event handler
draggable_imgs.forEach(image => {
    image.addEventListener("dragstart", dragStart);
});

// attach drop handlers for both sets of areas
// needed a different class name for the results one - so we can easily check for task completion later
const dropareas = document.querySelectorAll(".droparea, .resultsdroparea");
dropareas.forEach(box => {
    box.addEventListener("dragenter", dragEnter);
    box.addEventListener("dragover", dragOver);
    box.addEventListener("dragleave", dragLeave);
    box.addEventListener("drop", drop);
});

```

## CSS

```css
table, th, td {
  border: 2px solid #327ba8;
}

th {
  padding: 5px;
  text-align: center;
  text-align: -moz-center;
}

.drag-over {
  border: dashed 3px green;
}

.illegal-drop {
  border: dashed 3px red;
}

.draggable-image {
  max-width: 140px;
  max-height: 140px;
  display: block;
  margin: 5px 5px;
  cursor: pointer
}

.droparea, .resultsdroparea {
  width: 150px;
  height: 150px
}
```