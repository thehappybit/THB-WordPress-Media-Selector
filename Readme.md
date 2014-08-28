# WordPress Media Selector

This Javascript library helps theme and plugin developers to interact with the native WordPress media library modal window. It provides the means to customize modal texts, single/multiple selection and media library items type filter.

*Note: the WordPress Media Selector library is intended to be used with WordPress 3.5+*

## How to include the library in the WordPress admin

You can include the library script by attaching a function call to the `admin_enqueue_scripts` hook, e.g.

~~~~
function load_thb_media_selector_script() {
	wp_enqueue_media();
	wp_enqueue_script( 'thb_media_selector', 'path-to-thb.media_selector.js', array( 'jquery' ) );
}

add_action( 'admin_enqueue_scripts', 'load_thb_media_selector_script' );
~~~~

## Usage

Typically, you’ll want to invoke the library upon interacting with a UI control. In the event callback you would write:

~~~~
var media = new THB_MediaSelector( {
	select: function( selected_images ) {
		console.log( selected_images );
	}
} );

media.open();
// You can pass an array of attachments IDs, to pre-select them: media.open( [ 23, 145 ] );
// More than one value passed will only work if the 'multiple' option has been set to TRUE.
~~~~

## Options

The following options can be passed to the `THB_MediaSelector` call detailed above:

* **title**, the title of the media selection modal window.
* **button**, the text of the modal submit button.
* **type**, restrict items by type. Pick from: "", "image", "audio", "video".
* **multiple**, set to true to activate multiple selection.
* **close**, modal window close callback function. Fired when the modal window is closed without confirming the selection.
* **select**, modal window select callback function. Fired when the modal window is closed confirming the selection. The passed argument is an array containing the selected image(s).