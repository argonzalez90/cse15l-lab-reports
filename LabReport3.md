# Lab Report 3

## Failure Inducing Input
 > @Test
 public void testCaseInsensitiveSearchSuccess() throws URISyntaxException, IOException {

>   Handler h = new Handler("./technical/");

>    URI searchQuery = new URI("http://localhost/search?q=resonance");

>    String expected = "Found 2 paths:\n./technical/biomed/ar615.txt\n./technical/plos/journal.pbio.0020150.txt";

>    assertEquals(expected, h.handleRequest(searchQuery));
 }

## Does Not Induce Failure Input
>  @Test
 public void testSearchMismatchCase() throws URISyntaxException, IOException {

>  Handler h = new Handler("./technical/");

>    URI searchQueryMismatchCase = new URI("http://localhost/search?q=RESONANCE");

>    String expectedMismatchCase = "Found 2 paths:\n./technical/biomed/ar615.txt\n./technical/plos/journal.pbio.0020150.txt";

>    assertEquals(expectedMismatchCase, h.handleRequest(searchQueryMismatchCase));
 }

## Reason for Bug 
> The reason for this bug is due to `docsearch.java`utilizing `String.contains` and `Handler.handleRequest` which makes it case sensitive.

## Original code
> In the original line in `docsearch.java` the code looked like this `if(FileHelpers.readFile(f).contains(parameters[1])) {`

> After the fix it will look like this `if(FileHelpers.readFile(f).toLowerCase().contains(parameters[1].toLowerCase())) {`

