# isiau-digital-platform-api-doc
Technical documentation for ISIA Urbino Digital Platform API


Url address: https://dp.isiaurbino.net/api/
Querying: https://github.com/lykmapipo/express-mquery 

### API endpoint structure
The API endpoints are a mirror of the Digital Platform Google Drive's folder structure
```
+-- hello.gdoc
+-- xpub
|   +-- my-amazing-project
	|   +-- foo.gdoc
	|   +-- bar.jpg
``` 
So in above example the files are accessible via:
- https://dp.isiaurbino.net/api/hello
- https://dp.isiaurbino.net/api/xpub/my-amazing-project/foo
- https://dp.isiaurbino.net/api/xpub/my-amazing-project/bar

### File Entity (data fields)

```
{
	        {
      "metadata": {
        "dir": [string],
        "pinned": boolean,
        "id": string,
        "name": string,
        "mimeType": string,
        "starred": boolean,
        "createdTime": datetime,
        "modifiedTime": datetime,
        "published": boolean,
        "slug": string,
        "path": string,
        "trackingId": string,
        "fileExtension": string
      },
      "content": GDoc|GSheet|Video|Image|Audio|HTML|PDF,
      "_id": string,
    }
```
### CONTENT Types/Schema:
```
@Image
{  
  responsiveUrls: [String],  
  originalUrl: String,  
  alt: String,  
  title: String,  
  width: Number,  
  height: Number,  
  blurHash: {type: String, default: null}  
}
```
```
@Video
{  
  url: String,  
  source: String,  
  embed: String,  
  alt: String,  
  blurHash: {type: String, default: null},  
  width: Number,  
  height: Number,  
  originalName: String  
}
```
```
@Audio
{  
  alt: String,  
  originalUrl: String,  
  originalName: String,  
  remoteOnly: {type: Boolean, default: false},  
  urls: [
	  {  
        url: String,    
        format: {  
            ext: String,  
			type: String
        }  
    }]  
}
```
```
@Pdf
{  
  originalUrl: String,  
  alt: String,  
  remoteOnly: {type: Boolean, default: false}  
}
```
```
@HTML
{  
  originalUrl: String,  
  alt: String,  
  html: String,  
  text: String  
}
```

```
@Gdoc Content
{  
  text: String,  
  html: String,  
  images: [Image],  
  videos: [Video]
}
```
```
@GSheet Content
{  
    sheets:{  
      name: String,  
	  head: [String],  
	  rows: [[String]]  
    },  
  images: [Image]  
}
```

### Supported Mime Types
```
"application/vnd.google-apps.document",
"application/vnd.google-apps.spreadsheet",
"application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
"application/vnd.google-apps.folder",
"application/zip",
"application/pdf",
"text/csv",
"image/jpeg",
"image/jpg",
"image/png",
"image/gif",
"text/html",
"audio/mp3",
"audio/mpeg",
"audio/ogg",
"audio/wav",
"text/xml"
```

### resolving responsive images
Currently the api supports delivers images in two format:
- WebP
- JPG

And images are pre-processed into 3 sizes: 
`[1200, 800, 400]` 

In order to resolve the responsive url, simply add `.webp` or `.jpg` at the end of each of responsive urls. 

*Example*: 
[https://dp.isiaurbino.net/d3265830-742c-11ea-a8d9-0f8e727fda4c-1200w.webp](https://dp.isiaurbino.net/d3265830-742c-11ea-a8d9-0f8e727fda4c-1200w.webp)
