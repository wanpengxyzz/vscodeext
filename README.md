# vscodeext

comment for  monaco.editor
// The diff editor offers a navigator to jump between changes. Once the diff is computed the <em>next()</em> and <em>previous()</em> method allow navigation. By default setting the selection in the editor manually resets the navigation state.
var originalModel = monaco.editor.createModel("just some text\n\n\nHello World\n\nSome more text", "text/plain");
var modifiedModel = monaco.editor.createModel("just some Text\n\nHello World\n\nSome more changes", "text/plain");


var diffEditor = monaco.editor.createDiffEditor(document.getElementById("container"), {
	// You can optionally disable the resizing
	enableSplitViewResizing: false,
    dragAndDrop:true
});
diffEditor.setModel({
	original: originalModel,
	modified: modifiedModel
});
var viewZoneId = null;
diffEditor.getModifiedEditor().changeViewZones(function(changeAccessor) {
		var domNode = document.createElement('div');
        domNode.innerHTML = "hello";
		domNode.style.background = 'red';
		viewZoneId = changeAccessor.addZone({
					afterLineNumber: 4,
					// heightInLines: 4,
                    heightInPx: 100,
					domNode: domNode,
                    suppressMouseDown: true
		});
});
diffEditor.layout()
console.log(diffEditor.getModifiedEditor());
var navi = monaco.editor.createDiffNavigator(diffEditor, {
	followsCaret: true, // resets the navigator state when the user selects something in the editor
	ignoreCharChanges: true // jump from line to line
});

window.setInterval(function() {
	navi.next();
}, 2000);
