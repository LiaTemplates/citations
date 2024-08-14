<!--

script: https://cdnjs.cloudflare.com/ajax/libs/citation-js/0.7.15/citation.min.js

@onload
window.Cite = require('citation-js')
@end

@cite: @citeWithStyle(harvard1,```@0```)

@citeWithStyle
<script run-once modify="false">
let bibtexEntries = `@1`;

let example = new Cite(bibtexEntries)

console.log("XXXXXXXXXXXXX", example)

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

@BibliographyWithStyle
<script run-once modify="false">
let bibtexEntries = `@1`;

let example = new Cite(bibtexEntries)

console.log("XXXXXXXXXXXXX", example)

let output = example.format('bibliography', {
  format: 'html',
  template: `@0`,
  lang: 'en-US'
})

"HTML:"+output
</script>
@end


-->

# Test Citations

Das ist 
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
eine Referenz.


Das ist @cite(Q21972834) eine Referenz.

Hier kommt jetzt ein paragraph

```bibtex @BibliographyWithStyle(vancouver)
@book{johnson2019book,
  title={The Complete Guide to Examples},
  author={Johnson, Emily},
  year={2019},
  publisher={Academic Press},
  address={New York},
  url={https://doi.org/10.1000/conf.2021.123} 
}
```
