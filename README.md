# node-pluploader

Handles Plupload's chunked uploads so you don't have to.

## Example

```JavaScript
var Pluploader = require('node-pluploader');

// These options are also passed through to multiparty Form
// instances. See https://github.com/andrewrk/node-multiparty#multipartyform
var pluploader = new Pluploader({
  // Optional - defaults to 16. Expressed in MB
  uploadLimit: 16,
  // Optional - defaults to os.tmpDir()
  uploadDir: '/custom/upload-directory'
});

/*
  * Emitted when an entire file has been uploaded.
  *
  * @param file {Object} An object containing the uploaded file's name, type, buffered data & size
  * @param req {Request} The request that carried in the final chunk
  */
pluploader.on('fileUploaded', function(file, req) {
  console.log(file);
});

/*
  * Emitted when an error occurs
  *
  * @param error {Error} The error
  */
pluploader.on('error', function(error) {
    throw error;
});

// This example assumes you're using Express
app.post('/upload', function(req, res){
  pluploader.handleRequest(req, res);
});
```

