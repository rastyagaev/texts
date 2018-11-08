## Phase 1
### Make an ability to re-use code for url helpers (`model.picture.url(:version)``) we already have in views. Possible options:

* replace mount_uploader with some other method, which replicate current carrier_wave functionality for url helpers
**Pros:** get rid of carrier_wave
**Cons:** not clear how to test the whole application for possible errors after migration

* create carrier_wave adapter like we have for cloudinary — **it's a preferred option for now**
**Pros:** carrier_wave is good option for storing information about images/files versions, it's clear how to test — need to fulfill carrier_wave api using existing cloudinary adapter.
**Cons:** additional dependency (carrier_wave), it requires us to create an extra product, probably not so large, — uploadcare carrier_wave adapter.

### Uploaders

1. Find all places where we send a data file or a string to controllers, change it to uploadcare uploader
2. Mock all the conversion methods in carrier_wave, as well as all the uploading to the server.
3. Check every for with upload, don't lose any functionality (resizing, previewing, removing, editing).

### Migration (under consideration)

Duplicate every cloudinary attribute in every model with `<attribute_name>_cloudinary`, migrate cloudinary file to uploadcare.

### Output of phase to
Nothing was destructed, we have a general ability to use uploadcare and re-use current code (except uploaders).

## Phase 1
* Check every special case (like if we use url somehow else in code except carrier_wave url_helpers).
* Check the original files requirements
* Make tests for each special case

Output of phase 2 is ability to migrate the application by request.

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjI0Njk3NTQ5LDEwNzE1OTcxNDYsMjA2OT
A3MDkwNl19
-->