## drag-resize-snap

#### Provides the ability to drag, re-size, and snap any html element with pure javascript in only 6.37kb minified!

I needed a micro library in pure javascript (no jQuery) for draging,  resizeing, and  snapping.  
Found a great start [here](http://codepen.io/zz85/post/resizing-moving-snapping-windows-with-js-css) and heavily modified it to suite my needs:
 
Check out the [DEMO](http://codepen.io/arctelix/pen/RWVoMv)

#### installation:

Manually add drs.js to your project directory or download with Bower:

    bower install drag-resize-snap

Add drs.js to your project HTML:

    <script src="static/js/drs.js"></script>
    
Or use gitcdn:

    <script src="https://cdn.gitcdn.link/repo/arctelix/drag-resize-snap/master/dist/drs.js"></script>

NOTE: You can substitute `master` for a commit hash or version tag in your gitcdn urls

    <script src="https://cdn.gitcdn.link/repo/arctelix/drag-resize-snap/v0.1.1/dist/drs.js"></script>

#### Usage:

Simple config:

    var pane = document.getElementById('pane')
    var drs = core.util.DRS.makeDRS(pane)

Advanced config:

    // Create an element to drag, resize, and snap
    var pane = document.getElementById('pane')
    
    // (optional) Create an HTMLElement to use as a drag handle.
    // NOTE: Any child element of pane with class 'drag-area' will be added automatically.
    
    var handleOne = document.getElementById('some-id')
    
    // (optional) create a drag handle by absolutely positioned css rules (bounds).
    // Supply 4 sides or three sides and width or height to make four bounds.
    
    var handleTwo = {
        left:0, 			    // style.left
        bottom:28, 			  // style.bottom
        top:0, 				    // style.tip
        width:33, 			  // style.width
        right:null, 		  // style.right
        height:null, 		  // style.height
        invert: false,		// (false) true: Will invert the bounding box (areas not covered are dragable)
        hide: false,   		// (false) true: Will not append and HTMLelement for the area defined
    }
    
    // Specify options
    
    var options = {
        snapEdge: 5, 		  // (5) qty pixels pane needs to be moved beyond window to snap
        snapFull: 100, 	 	// (100) qty pixels pane needs to be moved beyond window to snap full screen
        resizeOuterM: 5, 	// (5) qty pixels outside pane bounds is dragable
        resizeInnerM: 8,  // (8) qty pixels inside pane bounds is dragable
    }
    
    // Apply the drag resize snap to your element
    
    var drs = core.util.DRS.makeDRS(pane, [handleOne , handleTwo], options)
    
#### See docs for more
    
Changes from original source to v0.1.1:
    
* Added a margin reduce when drag handle is clicked to avoid an un-snapable scenario.
* Zero SNAP_MARGINS contribute to un-snapable scenario. Added some protection for this as well.
Highly recommend SNAP_MARGIN of at lest 2 (5 is default), it provides same feel with less headache!
* Added tipple click to center and resize, another safe guard for un-snapable scenario.
* Separated DRAG_MARGINS and SNAP_MARGINS, thees need to be independent.
* Reduced code redundancy by adding getBounds().
* Added ability toggle pane bounds by percent of screen with convertUnits() & toggleUnits().
* Allow multiple drag handles and multiple types: (HTMLElement, bounds(css coordinates), and preset strings).
* Accept handle or array of mixed type handles at instantiation.
* Auto detect HTMLElements as handles with class 'drag-area'.
* Automatically create the ghostpane (never any reason to add it manually?).
* Created some api features snapFullScreen(), restorePreSnap(), center().
* Refactored canMove() to allow for customizable handle bounds.
* Automatically append HTML element for bounds handles.
* Refactored getHandleCoords() to allow for custom handle bounds & presets.
* Allow for inner and outer resize margins for better reliability, especially with corners.
* Allow for drag and resize with cursor hints when ele.style.pointer-events = "none".
* Refactored Calc() to allow for outer margins.
* Other tweaks...
