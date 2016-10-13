** KILN H5BP MODIFIED BOILER PLATE **
CURRENT BOILER PLATE VERSION: 0.2
	
	This boilerplate includes:	
		Bootstrap BP from initializr.com
			LAST UPDATED BY SI: 07/19/2016
			VERSION: 5.0
		Bootstrap
			LAST UPDATED BY SI: 07/19/2016
			VERSION: 3.3.1
		JQuery
			LAST UPDATED BY SI: 07/19/2016
			VERSION: 1.11.2
		Normalize CSS
			/* disabled by default, included in Bootstrap already */
			LAST UPDATED BY SI: 07/19/2016
			VERSION: 4.1.1
		Handlebars
			/* disabled by default, included for templatized customization in future versions */
			LAST UPDATED BY SI: 07/19/2016
			VERSION: 4.0.5
		Modernizr
			/* required by bootstrap, however not rolled into their files. when using BS, be sure to keep this file included */
			LAST UPDATED BY SI: 07/19/2016 
			VERSION: 2.8.3 (Responsive 1.4.2)
		Font Awesome
			LAST UPDATED BY SI: 07/19/2016
			VERSION: 4.6.3
		--prefix-free
			LAST UPDATED BY SI: 08/08/2016
			VERSION UNKNOWN

** NOTES **
	
	- STYLING

		kiln.css: this is where the most commonly used SI classes are stored, as well as extended bootstrap functionality.

		main.css: Each site should have custom styling added to main.css, avoiding modifying vendor or kiln css files. Overriding vendor files can be done here.

		The default for Kiln is to allow the CSS to cascade as follows:
			vendor < bootstrap < vendor < kiln < main < default < header < inline < !important

		The purpose is to allow bootstrap to take hierarchy over any vendor CSS, to ensure Bootstrap layout stays on page. In rare cases, some vendors may need to be in front of Bootstrap, however should never need to be loaded after kiln, main, or default. Kiln overrides some features of Bootstrap to allow for expanded Bootstrap functionality, while the main file is where we will build the client's website specific classes. Lastly, the default file is left blank for the client to use, moving forward after we've relinquished control to them. It is important that clients have the ability to override our design choices without digging through our CSS.

		If a style isn't applying correctly, more than likely bootstrap or kiln are taking precident, and you should add !important to the end of your declaration to force its override.

		Avoid using inline or on page css when possible, reserving this space for javascript or a client's custom HTML injections.

		- CLASS and ID NAMES
			kiln component class and id names will follow .SI_block--element--modifier{} and #SI_camelCase respectively to differentiate them from vendor classes.

			kiln utility class names will follow .SI_utility-function{}.

			To better understand component verse utility classes, read more here: http://davidtheclark.com/on-utility-classes/
			-"A component class encapsulates the declarations required to style an element within the context of a component."
			-"A utility class applies a single rule or a very simple, universal pattern."

		- COMPONENT CLASS NOMENCLATURE SPACING
			Blocks will be set to the beginning of the file, or indented once for their media query. Elements will be indented once after their respective block. Modifiers will be indented once beyond their element. Blocks will receive an extra line break to seperate them, while elements and modifiers will not:
			|	.SI_block{}
			|		.SI_block--element{}
			|			.SI_block--element--modifier{}
			|			.SI_block--element--modifier{}
			|		.SI_block--element{}
			|			.SI_block--element--modifier{}
			|			.SI_block--element--modifier{}
			|
			|	.SI_block{}
			|		.SI_block--element{}
			|		.SI_block--element{}
			|			.SI_block--element--modifier{}

		-EXTRA CLASSES AVAILABLE
			.SI_longBreak-10-xs - .SI_longBreak-100-xl
				Adds a margin to the bottom of the element equal to the number after longBreak-, in increments of ten. These are in mobile first design, and multiple can be added ( class="SI_longBreak-10-xs SI_longBreak-30-md SI_longBreak-50-lg", for example )
			.SI_breakToSpace-xs and .SI_breakToSpace-lg
				Turns a <br> into a space for xs and lower, and lg and larger, respectively. For example:
				<p>This sentence is in a header,<br class="SI_breakToSpace-xs">and needs a break on mobile only!</p>
				OUTPUT
				-MOBILE:
					This sentence is in a header,
					and needs a break on mobile only!
				-TABLET and LARGER:
					This sentence is in a header, and needs a break on mobile only!
			.SI_verticalAlign-xs
				Vertically aligns columns that sit next to each other, and should be added to the 'row' class of bootstrap elements. Works in Mobile-first design mode, and will cause the flow of bootstrap to break when the screen size is too small ( that is, class="col-xs-12 col-md-6" will not switch to 12 columns on resize. In this case, use SI_verticalAlign-md to allow the columns to wrap on XS sized screens ):
					<div class="column">
						<div class="row SI_verticalAlign-md">
							<div class="col-xs-12 col-md-6">
								ONE
							</div>
							<div class="col-xs-12 col-md-6">
								ONE<br>
								TWO<br>
								THR
							</div>
						</div>
					</div>
				OUTPUT
				-MOBILE:
					ONE
					ONE
					TWO
					THR
				-TABLET and LARGER:
						ONE
					ONE TWO
						THR

		-BOOTSTRAP EXTENSIONS
			.text-xs-left .text-xs-right .text-xs-center and .text-xs-justify
				Allows text alignment based on Bootstraps breakpoints. Follows mobile first design mode
			.five-row .seven-row .nine-row and .eleven-row
				Allows 5, 7, 9 or 11 column based rows, as opposed to the bootstrap 12 default. This class should be added to bootstraps default 'row', and then all other bootstrap classes stay the same. For example:
					<div class="column">
						<div class="row nine-row">
							<div class="col-xs-9 col-md-4">
								ONE
							</div>
							<div class="col-xs-9 col-md-5">
								ONE<br>
								TWO<br>
								THR
							</div>
						</div>
					</div>
				OUTPUT
				-MOBILE:
					ONE
					ONE
					TWO
					THR
				-TABLET and LARGER:
					ONE 			ONE
									TWO
									THR

	- JAVASCRIPT
		Javascript runs out of the js/vendors/ folder where appropriate. 

		SI added custom functionality should be added to js/kiln/kiln.js, and should follow the convention SI_camelCase(); utilizing the SI_ prefix to delineate custom functions produced by the SI team.

		Site specific functions should be stored under js/main.js and should be given a prefix to insure they do not interfere with vendor functionality. Whenever possible, functions should be modularized and added to the kiln.js file in order to maintain a repository of useful functions created by SI. When doing so, remember to notify other users of the change, and modify the shared kiln folder.

	-HTML TEMPLATE COMPONENTS
		Located in the index.html file, and marked by <!-- COMMENTS -->, these pieces are reusable HTML blocks that can be stacked to quickly form the layout of the page, and then later stylized.

	    - NAVBAR
			By default, the navbar is stickied at 50px. When changing the height of the navbar, modify the <style>body{padding-top:50px;}</style> located in the <head> element. The navbar sits outside of the document's flow, and will cover the top of the document if not properly modified.

		- HERO SECTION
			A bootstrap jumbotron used to create a hero image at the top of a document. Should be outside of the content .container.

