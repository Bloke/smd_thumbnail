# smd_thumbnail

h1. smd_thumbnail

h2. Features

* Assign any number of thumbnails to Txp's images
* Batch assign thumbnails to existing images
* Set one thumbnail size as default
* Display any of the thumbnail sizes on your site
* Keep thumbs in sync with Txp's thumbs if you wish
* Conditional thumbnail check available

h2. Installation / upgrading / uninstallation

p(warning). Requires Txp 4.5.0+

Download the plugin from either "textpattern.org":http://textpattern.org/plugins/1186/smd_thumbnail, or the "software page":http://stefdawson.com/sw, paste the code into the Txp Admin -> Plugins pane, install and enable the plugin. Visit the "forum thread":http://forum.textpattern.com/viewtopic.php?id=34367 for more info or to report on the success or otherwise of the plugin.

p(warning). When upgrading froim v0.1x to v0.20, your preferences for _Keep Txp thumbnails in sync with default profile_ will be removed. Please visit the _Tools/Prefs_ area to reinstate the behaviour you desire.

To uninstall, delete from the Admin -> Plugins page.

h2. Usage -- admin side

Visit the Content->Images tab. Above the list of images is an area labelled _Thumbnail Profiles_. Click it to reveal the control panel. You can toggle this panel on and off by clicking the heading.

You must define at least one profile to begin with, so click the _New profile_ button. This will reveal edit boxes where you can enter:

* *Name*: some descriptive name for this thumbnail dimension. You are limited to usual non-weird characters in the name
* *Width*: thumbnail width, in pixels. If left blank (or set to 0) and height is specified, the width will be computed in proportion to the height
* *Height*: thumbnail height, in pixels. If left blank (or set to 0) and width is specified, the height will be computed in proportion to the width
* *Quality (%)*: The quality of the resulting thumbnail. Generally only of use for jpg or png(24) images. The higher the value the better the quality and the bigger the file size. Default: 75
* *Crop*: whether to crop the image when the thumbnail is created, or scale it to fit
* *Sharpen*: whether to apply a sharpening filter to the thumbnail when it is created. Useful for very small images
* *Active*: Enable/disable this thumbnail size so it will/won't be automatically generated when the next image is uploaded. Click the checkbox to instantly switch the profile on/off. Click the 'Active' word in the heading row to toggle the status of all profiles. Note that this setting governs how the "All sizes":#smd_thumb_create dropdown entry interacts with the _Create_ and _Delete_ buttons
* *Default*: set this thumbnail profile as the default. The default image will be displayed in the Images list and will also be used as the default size to be displayed using @<txp:smd_thumbnail/>@. If the option to "sync with Txp's thumbs":#smd_thumb_prefs is on, it will also become Txp's standard (built-in) thumbnail size from this point forward

Once you've configured your profile, click Save to store it. You can always edit it again by clicking its name. Go ahead and create some more profiles for thumbnails of different sizes/parameters. If you wish to delete a profile, hit the _[Delete]_ button and confirm. *All thumbnails associated with that profile will be deleted*.

At this point, no thumbnails have been created. Let's rectify that.

h3(#smd_thumb_create). Creating thumbnails

Pick one of your images and click to edit it.

Beneath the main picture you will see an area labelled _Thumbnails_. You can toggle this panel on and off by clicking the heading.

Inside the panel is a simple select list containing one entry for each thumbnail profile you have configured, plus the special entry _All sizes_. You can select one of these entries and click _Create_ to create thumbnail(s) in the selected size or hit _Delete_ to remove the selected thumbnail(s).

Once created, the thumbnails appear in the panel; remember they can be tucked away if you don't want to look at them.

If you select _All sizes_ and hit _Create_, you will get one thumbnail for each active profile. Similarly, if you hit _Delete_ any thumbnails stored against an active profile for the current image will be removed. By toggling certain thumbnail profiles on/off you can control which ones are created or deleted.

By default:

* when you upload a new image, thumbnails will be automatically created for any active profiles
* when you replace an existing image, thumbnails will only be automatically created for active profiles if thumbs _do not_ already exist. This option can be altered with the "prefs":#smd_thumb_prefs

Note that if you use Txp's multi-edit tool to delete images, *all* corresponding thumbnails for the selected images (including inactive ones) will be removed.

h3(#smd_thumb_custom). Custom thumbnails

If you prefer to make your own thumbs in an external program, you can still set up the profiles as normal but instead of clicking _Create_ in the Image Edit screen, you can pick a profile size from the dropdown and use the file picker facility (Browse... / Choose...) to select a thumbnail from your hard drive. When you click _Upload_ the image will be inserted against the selected profile.

At any time you can click one of the thumbnails (or select a size from the dropdown) and choose for another image to replace the existing thumbnail -- even ones that have been auto-created. Some things to note about this feature:

* the thumbnail must be of the same file type as the original image or the upload will be ignored
* you can click a highlighted image to deselect it
* you cannot Browse for an image (the file upload box is greyed out) unless you have chosen one profile

h3(#smd_thumb_batch). Batch thumbnail creation

You can also create thumbnails en-masse. Click the _Tools_ button (labelled '_Tools / Prefs_' if you have sufficient rights) in the top-right hand corner of the smd_thumbnail control panel. From there you will see an area that allows you to create thumbnails for:

* Only the selected images (the checkboxes next to each image)
* All images of a particular category
* All images uploaded by a particular user
* All images

After selecting the desired option (and if you choose category or author, select one of the entries from the secondary list that apears), hit _Create_. Once you confirm your action, the plugin will go away and create thumbnails for every active profile for all images that match your criteria. This is a quick way to generate thumbs for your existing images. Note that if you choose the first (empty) category entry, then all images that have not been assigned a category are manipulated.

Because of the nature of this tool -- especially with large image pools -- the process is done as a background task via AJAX. After clicking the _Create_ button (and confirming you are sure) a counter will appear in the top-right of the prefs panel showing how many images it has processed out of the total number of images in the set. When it's done, if you then refresh your Images tab (e.g. click to the _Profiles_ pane) you will see your chosen default thumbnails in the list -- assuming you've set one as default.

h3(#smd_thumb_prefs). Preferences

If you have sufficient privileges, in the lower portion of the _Tools_ panel are some options that govern how thumbnails are created for all users. There is no 'Save' action here: the checkmarks are stored in real-time and always reflect the current state.

h4. Create smd_thumbnails from

Governs whether the smd_thumbnails are created from the full size image or its (Txp) thumbnail. If you have elected not to have Txp thumbnails created then it'll probably not work very well :-)

This preference applies:

* when you use any of the batch tools to mass-produce smd_thumbnails
* if you upload a new image
* if you reupload a main image and _Recreate thumbnails on re-upload of main image_ is checked

h4. Keep Txp thumbnails in sync with default profile

(This option only appears if you have set a profile as default)

Ordinarily, smd_thumbnail works independently of Txp's thumbs. If you disable the plugin you'll see that everything goes back to how it was before you installed it. This is great because your hard-graft isn't lost if you have uploaded your own thumbs.

But if you start creating thumbs with the plugin you will notice that Txp's built in tags such as @<txp:article_image thumbnail="1" />@ and @<txp:thumbnail />@ won't work for newer thumbnails. This might be confusing so you can opt to have smd_thumbnail update your Txp thumbnails at the same time.

By ticking either of the checkboxes, the plugin will track any changes *to the default profile* and mimic them with Txp's thumbnails. This has a few effects worth highlighting.

When the _Creation_ checkbox is ticked:

# if you batch create thumbs, upload a new image, or replace an existing image, a new Txp thumbnail will be created at the default size. Any existing thumbs will be overwritten
# if you change default profile, any Txp thumbnails that have been created will remain at the previous size. Only when you start creating, uploading or replacing images will the new thumbnail sizes be created

When the _Deletion_ checkbox is ticked:

# if you delete a single thumb that corresponds to the default profile, both the profile thumb and Txp's thumb will be deleted
# if you delete an entire profile, all its thumbnails *and all Txp's thumbs* will be removed

Further:

# if you have no default profile, the checkboxes disappear and the settings have no effect. Choose a default profile to reinstate the behaviour
# if you deactivate the default profile the checkboxes have no effect *unless* you delete the profile (since you're deleting it, its status is 'lost' and therefore the checkboxes function as normal). If there's any doubt, uncheck the _Deletion_ checkbox first!

h4. Recreate thumbnails on re-upload of main image

When this checkbox is cleared and you *replace* a main image (from the Image Edit screen) any thumbnails that have already been assigned to the image are left as they are -- only missing thumbnails will be created from the main image. Conversely, if you set this checkbox, when you upload the replacement image *ALL smd_thumbnails for active profiles will be (re)created from the main image*.

Note one important exception: Txp thumbnails are *NOT* covered by this option -- they are governed by the _Keep Txp thumbs in sync_'s 'Creation' checkbox. Thus, if you upload a replacement image and the 'Creation' checkbox is on, you will replace Txp's thumb regardless of the setting of the _Recreate thumbnails..._ option.

h2(#smd_thumbnail). Tag: @<txp:smd_thumbnail />@

A direct replacement for the built in "txp:thumbnail":http://textpattern.net/wiki/index.php?title=thumbnail tag with exactly the same functionality and attributes apart from these exceptions:

* %(atnm)type% : use this attribute to display thumbnails of the given profile name. e.g. @type="large"@. If you do not specify this attribute, the default profile will be used. If there is no default profile you'll see warning messages
* %(atnm)class% : if omitted, the name of the profile will be used as a class name for the img tag. If you specify a wraptag and omit the class, the profile name will be used as a class on both the container and the img tag
* %(atnm)align% : this attribute has been removed
* %(atnm)add_stamp% : adds the image file modification time to the end of the thumbnail's URL. Use @add_stamp="1"@ to switch this feature on. This helps prevent stale images, but may prevent browsers from cacheing the thumbs properly thus increasing bandwidth usage. Default: 0
* %(atnm)force_size% : usually when you set one or other width/height to 0 in a profile, the browser scales the missing dimension automatically. It does this by omitting the @width=@ or @height=@ attribute in the @<img>@ tag. This may cause visual artefacts as the page is rendered and the browser calculates the sizes. If you wish the plugin to add the actual dimension to the @<img>@ tag (the size at the time the thumbnail was created), tell the plugin with this attribute. Choose one or both of @width@ or @height@. Comma-separate as required. Default: unset
* %(atnm)display% : by default, this tag outputs a full @<img>@ tag. If you just require the image URL so you can make your own image tags, set @display="url"@. Default: @thumbnail@
* %(atnm)form% : you can construct your own @<img>@ tags using the given form. If not specified, you may use the tag as a container.

The tag works inside @<txp:images>@ or can be used standalone by specifying the @id@ or @name@ attribute. If using it as a container or with the @form@ attribute you display the various pieces of thumbnail information using the @<txp:smd_thumbnail_info>@ tag.

h2(#smd_thumbnail_info). Tag: @<txp:smd_thumbnail_info />@

Display various information from the current @<txp:smd_thumbnail>@ tag (in either its form or container). Attributes:

* %(atnm)item% : list of things you wish to display. Choose from:
** @url@ : full image URL of the thumbnail
** @type@ : thumbnail profile name
** @name@ : image name
** @id@ : thumbnail ID
** @ext@ : thumbnail file extension
** @category@ : image category name
** @category_title@ : image category title
** @alt@ : image alt text
** @title@ : image title / caption
** @author@ : image author
** @class@ : class applied to thumbnail (if not supplied, is same as type)
** @date@ : raw datestamp of when the image was uploaded
** @w@ : thumbnail width (pixels)
** @h@ : thumbnail height (pixels)
** @html_w@ : HTML-formatted width attribute
** @html_h@ : HTML-formatted height attribute
* %(atnm)wraptag% : HTML tag, without angle brackets, to wrap all the items with. e.g. @wraptag="ul"@
* %(atnm)class% : CSS class name to apply to the wraptag
* %(atnm)break% : HTML tag, without angle brackets, to wrap each item with. e.g. @break="li"@

h2(#smd_if_thumbnail). Tag: @<txp:smd_if_thumbnail>@

A direct replacement for the built in @<txp:if_thumbnail />@ tag with exactly the same functionality. It has one attribute:

* %(atnm)type% : use this attribute to check for thumbnails of the given profile name. e.g. @type="Medium"@. If you do not specify this attribute, the default profile will be tested. If there is no default profile the tag will always render the @<txp:else />@ portion

h2(#smd_thumb_how_it_works). How it works

For reference, when you create a profile a directory is created with that name inside your Txp @images@ folder. Inside this folder you will find images of the format @id.ext@: where @id@ and @ext@ match the corresponding image IDs in the Txp database. That's pretty much it.

You can delete thumbnail files manually from any of these directories and the plugin will figure everything out. But it's probably not advisable to delete the directories themselves -- use the _[Delete]_ buttons in the control panel for that.

h2. Author / credits

Written by "Stef Dawson":http://stefdawson.com/contact. Many thanks to the beta test crew who offered feature and workflow advice, especially thebombsite, jakob, jstubbs and maniqui.

h2(#smd_thumb_changelog). Changelog

* 26 Sep 2014 | 0.31 | Selected thumbnail creation for 4.6.x (thanks jpdupont)
* 14 Jan 2013 | 0.30 | For Txp 4.5.0 ; added mem_moderation_image support ; smd_thumbnail tag has form/container support ; added smd_thumbnail_info tag ; fixed image <-> select list interaction (damn you attr/prop!) ; added better tooltip on thumb hover ; fixed invalid markup ; added width & height attributes (thanks jstubbs)
* 12 Oct 2011 | 0.22 | Added @display@ attribute ; added 'create from' preference (thanks the blue dragon/maniqui) ; fixed plugin for dashboard use ; fixed jQuery attr/prop in prefs ; fixed Txp menu interference (thanks maniqui)
* 12 May 2011 | 0.21 | Added @smd_thumb_get_profiles()@ for other plugins to find which profiles are available
* 26 Jan 2011 | 0.20 | Tools / prefs separated from profile list ; permitted batch creation via 1) selected images 2) category 3) author (thanks jpdupont) ; added smd_thumb_auto_replace option and altered default behaviour (thanks maniqui) ; fixed Txp thumbnail creation on thumbnail replace and made prefs global -- and only available to site admins (all thanks jstubbs) ; fixed New Profile button wrapping (thanks jpdupont)
* 21 Nov 2010 | 0.14 | Permitted thumbs to be larger than the original images (thanks maniqui) ; fixed callbacks for image uploading and deleting
* 10 Nov 2010 | 0.13 | Added confirmation on _Create all_ ; relabelled upload box (thank uli) ; tamed styles ; silenced chmod warnings (thanks zero)
* 10 Nov 2010 | 0.12 | Added ability to sync default profile thumbs with the corresponding Txp thumbnails (thanks zero)
* 09 Nov 2010 | 0.11 | Added @force_size@ and @add_stamp@ (both thanks zero) ; removed unnecessary DB call
* 04 Oct 2010 | 0.10 | Official public release
* 06 Aug 2010 | 0.10beta | Initial beta release