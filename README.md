<!--

author:  André Dietrich, Sebastian Zug

email:   LiaScript@web.de

version: 0.0.1

comment: This is a simple plugin for embedding bibtex based references in LiaScript materials.

script: https://cdnjs.cloudflare.com/ajax/libs/citation-js/0.7.15/citation.min.js

@onload
window.Cite = require('citation-js')
@end

@cite: @citeWithStyle(harvard1,```@0```)

@citeWithStyle
<script run-once modify="false">
let bibtexEntries = `@1`;

let example = new Cite(bibtexEntries)

let output = example.format('citation', {
  format: 'html',
  template: `@0`,
  lang: 'en-US'
})

let url = bibtexEntries.match(/url=\{([^\}]+)/)
if (url && url.length > 1) 
{
    output = `<a href="${url[1]}" target="blank_">${output}</a>`
}

"HTML:"+output
</script>
@end

@bibliography: @bibliographyWithStyle(harvard1,```@0```)

@bibliographyWithStyle
<script run-once modify="false">
let bibtexEntries = `@1`;

let example = new Cite(bibtexEntries)

let output = example.format('bibliography', {
  format: 'html',
  template: `@0`,
  lang: 'en-US'
})

"HTML:"+output
</script>
@end


@bibliographyWithStyleFromFile
<script run-once modify="false">

function fetchFileContent(url) {
  return fetch(url)
    .then(function(response) {
      if (!response.ok) {
          throw new Error('HTTP error! status: ' + response.status);
      }
      return response.blob();
    })
    .then(function(blob) {
      return new Promise(function(resolve, reject) {
        var reader = new FileReader();
        reader.onloadend = function() {
            resolve(reader.result);
        };
        reader.onerror = function() {
            reject('Error reading the file');
        };
        reader.readAsText(blob); // oder 'readAsArrayBuffer(blob)' für Binärdaten
      });
    })
    .catch(function(error) {
      console.error('Es gab einen Fehler beim Abrufen der Datei:', error);
      return null;
    });
}

fetchFileContent(https://raw.githubusercontent.com/LiaTemplates/citations/main/bibtex.bib)
    .then(function(content) {
        let references = content
        console.log("************************************************");
        console.log('Dateiinhalt:', references);
    });


</script>
@end

-->

# Embedded Bibtex Citations

    --{{0}}--
This plugin supports the use of Bibtex-based references. The user can either specify the corresponding literature sources directly in the LiaScript document or store them in a separate file and address them using a URL.

This LiaScript plugin uses the [citation_js](https://citation.js.org/) implementation of  L. G.Willighagen. Many thanks for his great work 

@bibliography(10.5281/zenodo.1005176)

**Try it on LiaScript:**

https://liascript.github.io/course/?https://raw.githubusercontent.com/LiaTemplates/citations/main/README.md

See the project on Github:

https://github.com/LiaTemplates/CollaborativeDrawing

    --{{1}}--
There are three ways to use this template.
The easiest way is to use the import statement and the url of the raw text-file of the master branch or any other branch or version.
But you can also copy the required functionality directly into the header of your Markdown document, see therefor the last slide.
And of course, you could also clone this project and change it, as you wish.

      {{1}}

- Load the macros via and set the persistence flag to true.
  Persistent will guarantee, that your drawings will be updated, even if you are on another slide.

  ```text
  import: https://raw.githubusercontent.com/LiaTemplates/citations/main/README.md

  ```

  or use the tagged version:

  ```text
  import: https://raw.githubusercontent.com/LiaTemplates/citations/main/0.0.1/README.md
  ```

- Copy the definitions into your Project

- Clone this repository on GitHub

## Overview on citation_js

1. The **representation*** can be 

    + `cite` - short key reference
       @cite(https://doi.org/10.1080/08993408.2022.2029046)
    
    + `bibliography` - detailed reference
       @bibliography(https://doi.org/10.1080/08993408.2022.2029046)

2. The current implementation distinguishes the user patterns in three directions: Currently just three **styles of documents** are supported#️⃣

    + `ieee` @bibliographyWithStyle(ieee, 10.5281/zenodo.1005176)
    
    + `vancouver` @bibliographyWithStyle(vancouver, 10.5281/zenodo.1005176)
    
    + `harvard1` @bibliographyWithStyle(harvard1, 10.5281/zenodo.1005176)

    The pattern is adressed by calling `bibliographyWithStyle()` or `citeWithStyle()`. The short term versions `bibliography` or `cite` use `harvard1` as default value.

3. The reference data may be recorded directly in the document or in a separate file. This can then be read in via the URL. The corresponding versions `bibliographyWithStyleFromFile` or `citeWithStyleFromFile()` have two parameters, the style pattern from (2) and a url representing a bibtexfile.

## Usage examples

`@cite`

````
```bibtex @cite
@book{johnson2019book,
  title={The Complete Guide to Examples},
  author={Johnson, Emily},
  year={2019},
  publisher={Academic Press},
  address={New York},
  url={https://doi.org/10.1000/conf.2021.123} 
}
```
````

The link of the reference points at the corresponding website.

```bibtex @cite
@book{johnson2019book,
  title={The Complete Guide to Examples},
  author={Johnson, Emily},
  year={2019},
  publisher={Academic Press},
  address={New York},
  url={https://doi.org/10.1000/conf.2021.123} 
}
```

-------------------------------------------------------------------------------

`@bibliographyWithStyle`

````
```bibtex @bibliographyWithStyle(ieee)
@book{johnson2019book,
  title={The Complete Guide to Examples},
  author={Johnson, Emily},
  year={2019},
  publisher={Academic Press},
  address={New York},
  url={https://doi.org/10.1000/conf.2021.123} 
}
```
````

The link of the reference points at the corresponding website.

```bibtex @bibliographyWithStyle(ieee)
@book{johnson2019book,
  title={The Complete Guide to Examples},
  author={Johnson, Emily},
  year={2019},
  publisher={Academic Press},
  address={New York},
  url={https://doi.org/10.1000/conf.2021.123} 
}
```

-------------------------------------------------------------------------------

`@bibliographyWithStyleFromFile`


```
@bibliographyfromFile(https://raw.githubusercontent.com/LiaTemplates/citations/main/bibtex.bib)
```

@bibliographyfromFile(https://raw.githubusercontent.com/LiaTemplates/citations/main/bibtex.bib)
