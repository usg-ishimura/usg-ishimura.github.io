---
author: John Doe
facebook_username: john.doe
twitter_username: johndoe
google_username: johndoe
linkedin_username: johndoe
instagram_username: johndoe
github_username: johndoe
tags: "jekyll python json powershell" 
---

## Blog Post Title From First Header

Due to a plugin called `jekyll-titles-from-headings` which is supported by GitHub Pages by default. The above header (in the markdown file) will be automatically used as the pages title.

If the file does not start with a header, then the post title will be derived from the filename.

This is a sample blog post. You can talk about all sorts of fun things here.

---

### This is a header

#### Some PowerShell Code

```powershell
Write-Host "This is a powershell Code block";

# There are many other languages you can use, but the style has to be loaded first

ForEach ($thing in $things) {
    Write-Output "It highlights it using the GitHub style"
}
```

#### Json Snippet

```json
{
  "721": {
    "bc8cbfe404d5d4b70ab68290c4ecda517c27a7a547aa367ae16c8490": {
      "dCNFTvsCSP": {
        "name": "Stuck in 305",
        "image": "ipfs://QmVMC5CcSKtqwCnniY348AcGw8aHtJqazodDMXYqoXJgtX/dvsc.jpg",
        "files": [
          {
            "name": "Cardano BOT",
            "mediaType": "text/html",
            "src": "ipfs://QmVMC5CcSKtqwCnniY348AcGw8aHtJqazodDMXYqoXJgtX/c_b.html"
          },
          {
            "name": "Description",
            "mediaType": "text/html",
            "src": "ipfs://QmVMC5CcSKtqwCnniY348AcGw8aHtJqazodDMXYqoXJgtX/dsc.html"
          }
        ],
        "Running dynamic cnft on ipfs gateway": "ipfs://QmVMC5CcSKtqwCnniY348AcGw8aHtJqazodDMXYqoXJgtX/c_b.html",
        "Firefox mheadercontrol add on": "ipfs://QmVMC5CcSKtqwCnniY348AcGw8aHtJqazodDMXYqoXJgtX/f_r.html",
        "chrome always disable csp add on": "ipfs://QmVMC5CcSKtqwCnniY348AcGw8aHtJqazodDMXYqoXJgtX/c_r.html"
      }
    }
  }
}
```
#### Python Hello World

```python
#!/usr/bin/env python3
from http.server import HTTPServer, SimpleHTTPRequestHandler, test
import sys

class CORSRequestHandler (SimpleHTTPRequestHandler):
    def end_headers (self):
        self.send_header('Access-Control-Allow-Origin', '*')
        SimpleHTTPRequestHandler.end_headers(self)

if __name__ == '__main__':
    test(CORSRequestHandler, HTTPServer, port=int(sys.argv[1]) if len(sys.argv) > 1 else 8000)
```
