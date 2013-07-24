The purpose of this code is to set up watchers for attribute changes on DOM elements.

If I have an element `document.querySelector('#target')`

And I want to watch for property changes:

	target.setAttribute("name", "bar");
	target.setAttribute("name", "baz");

I would do this:

	//	Create new observer object
	//
	var observer = new MutationObserver(function(mutations) {
		//	Display the change data when it happens.
		//
		mutations.forEach(function(mutation) {
			for(var p in mutation) {
				console.log(p + " = " + mutation[p]);
			}
		});    
	});
	
	//	These are only relevant to non-IE implementations
	//
	var config = { 
		attributes			: true, 
		childList			: true, 
		characterData		: true,
		attributeOldValue	: true
	}
	
	//	Watch for prop changes on an element
	//
	var target = document.querySelector('#target');
	observer.observe(target, config);