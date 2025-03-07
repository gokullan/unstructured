<h3 align="center">
  <img
    src="https://raw.githubusercontent.com/Unstructured-IO/unstructured/main/img/unstructured_logo.png"
    height="200"
  >
</h3>

<div align="center">

  <a href="https://github.com/Unstructured-IO/unstructured/blob/main/LICENSE.md">![https://pypi.python.org/pypi/unstructured/](https://img.shields.io/pypi/l/unstructured.svg)</a>
  <a href="https://pypi.python.org/pypi/unstructured/">![https://pypi.python.org/pypi/unstructured/](https://img.shields.io/pypi/pyversions/unstructured.svg)</a>
  <a href="https://GitHub.com/unstructured-io/unstructured/graphs/contributors">![https://GitHub.com/unstructured-io/unstructured.js/graphs/contributors](https://img.shields.io/github/contributors/unstructured-io/unstructured)</a>
  <a href="https://github.com/Unstructured-IO/unstructured/blob/main/CODE_OF_CONDUCT.md">![code_of_conduct.md](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg) </a>
  <a href="https://GitHub.com/unstructured-io/unstructured/releases">![https://GitHub.com/unstructured-io/unstructured.js/releases](https://img.shields.io/github/release/unstructured-io/unstructured)</a>
  <a href="https://pypi.python.org/pypi/unstructured/">![https://github.com/Naereen/badges/](https://badgen.net/badge/Open%20Source%20%3F/Yes%21/blue?icon=github)</a>

</div>

<div align="center">
<img src="https://user-images.githubusercontent.com/38184042/205945013-99670127-0bf3-4851-b4ac-0bc23e357476.gif" title="unstructured in action!">
</div>

<h3 align="center">
  <p>Open-Source Pre-Processing Tools for Unstructured Data</p>
</h3>


The `unstructured` library provides open-source components for pre-processing text documents
such as **PDFs**, **HTML** and **Word** Documents. These components are packaged as *bricks* 🧱, which provide
users the building blocks they need to build pipelines targeted at the documents they care
about. Bricks in the library fall into three categories:

- :jigsaw: ***Partitioning bricks*** that break raw documents down into standard, structured
  elements.
- :broom: ***Cleaning bricks*** that remove unwanted text from documents, such as boilerplate and
  sentence
  fragments.
- :performing_arts: ***Staging bricks*** that format data for downstream tasks, such as ML inference
  and data labeling.
<br></br>
## :eight_pointed_black_star: Installation

To install the library, run `pip install unstructured`.

## :coffee: Getting Started

* Using `pyenv` to manage virtualenv's is recommended but not necessary
	* Mac install instructions. See [here](https://github.com/Unstructured-IO/community#mac--homebrew) for more detailed instructions.
		* `brew install pyenv-virtualenv`
	  * `pyenv install 3.8.15`
  * Linux instructions are available [here](https://github.com/Unstructured-IO/community#linux).

* Create a virtualenv to work in and activate it, e.g. for one named `unstructured`:

	`pyenv  virtualenv 3.8.15 unstructured` <br />
	`pyenv activate unstructured`

* Run `make install-project-local`

## :clap: Quick Tour

You can run this [Colab notebook](https://colab.research.google.com/drive/1RnXEiSTUaru8vZSGbh1U2T2P9aUa5tQD#scrollTo=E_WN7p3JGcLJ) to run the examples below.

The following examples show how to get started with the `unstructured` library.
You can parse **TXT**, **HTML**, **PDF**, **EML** and **DOCX** documents with one line of code!
<br></br>
See our [documentation page](https://unstructured-io.github.io/unstructured) for a full description
of the features in the library.

### Document Parsing

The easiest way to parse a document in unstructured is to use the `partition` brick. If you
use `partition` brick, `unstructured` will detect the file type and route it to the appropriate
file-specific partitioning brick.
If you are using the `partition` brick, ensure you first install `libmagic` using the
instructions outlined [here](https://unstructured-io.github.io/unstructured/installing.html#filetype-detection)
`partition` will always apply the default arguments. If you need
advanced features, use a document-specific brick. The `partition` brick currently works for
`.txt`, `.docx`, `eml`, `.html`, and `.pdf` documents.

```python
from unstructured.partition.auto import partition

elements = partition("example-docs/layout-parser-paper.pdf")
```

Run `print("\n\n".join([str(el) for el in elements]))` to get a string representation of the
output, which looks like:

```

LayoutParser : A Uniﬁed Toolkit for Deep Learning Based Document Image Analysis

Zejiang Shen 1 ( (cid:0) ), Ruochen Zhang 2 , Melissa Dell 3 , Benjamin Charles Germain Lee 4 , Jacob Carlson 3 , and
Weining Li 5

Abstract. Recent advances in document image analysis (DIA) have been primarily driven by the application of neural
networks. Ideally, research outcomes could be easily deployed in production and extended for further investigation.
However, various factors like loosely organized codebases and sophisticated model conﬁgurations complicate the easy
reuse of im- portant innovations by a wide audience. Though there have been on-going eﬀorts to improve reusability and
simplify deep learning (DL) model development in disciplines like natural language processing and computer vision, none
of them are optimized for challenges in the domain of DIA. This represents a major gap in the existing toolkit, as DIA
is central to academic research across a wide range of disciplines in the social sciences and humanities. This paper
introduces LayoutParser , an open-source library for streamlining the usage of DL in DIA research and applica- tions.
The core LayoutParser library comes with a set of simple and intuitive interfaces for applying and customizing DL models
for layout de- tection, character recognition, and many other document processing tasks. To promote extensibility,
LayoutParser also incorporates a community platform for sharing both pre-trained models and full document digiti- zation
pipelines. We demonstrate that LayoutParser is helpful for both lightweight and large-scale digitization pipelines in
real-word use cases. The library is publicly available at https://layout-parser.github.io

Keywords: Document Image Analysis · Deep Learning · Layout Analysis · Character Recognition · Open Source library ·
Toolkit.

Introduction

Deep Learning(DL)-based approaches are the state-of-the-art for a wide range of document image analysis (DIA) tasks
including document image classiﬁcation [11,
```

### HTML Parsing

You can parse an HTML document using the following workflow:

```python
from unstructured.partition.html import partition_html

elements = partition_html("example-docs/example-10k.html")
print("\n\n".join([str(el) for el in elements[:5]]))
```

The print statement will show the following text:
```
UNITED STATES

SECURITIES AND EXCHANGE COMMISSION

Washington, D.C. 20549

FORM 10-K

ANNUAL REPORT PURSUANT TO SECTION 13 OR 15(d) OF THE SECURITIES EXCHANGE ACT OF 1934
```

And `elements` will be a list of elements in the HTML document, similar to the following:

```python
[<unstructured.documents.elements.Title at 0x169cbe820>,
 <unstructured.documents.elements.NarrativeText at 0x169cbe8e0>,
 <unstructured.documents.elements.NarrativeText at 0x169cbe3a0>]
```

### PDF Parsing

You can use the following workflow to parse PDF documents.

```python
from unstructured.partition.pdf import partition_pdf

elements = partition_pdf("example-docs/layout-parser-paper.pdf")
```

The output will look the same as the example from the document parsing section above.


### E-mail Parsing

The `partition_email` function within `unstructured` is helpful for parsing `.eml` files. Common
e-mail clients such as Microsoft Outlook and Gmail support exproting e-mails as `.eml` files.
`partition_email` accepts filenames, file-like object, and raw text as input. The following
three snippets for parsing `.eml` files are equivalent:

```python
from unstructured.partition.email import partition_email

elements = partition_email(filename="example-docs/fake-email.eml")

with open("example-docs/fake-email.eml", "r") as f:
  elements = partition_email(file=f)

with open("example-docs/fake-email.eml", "r") as f:
  text = f.read()
elements = partition_email(text=text)
```

The `elements` output will look like the following:

```python
[<unstructured.documents.html.HTMLNarrativeText at 0x13ab14370>,
<unstructured.documents.html.HTMLTitle at 0x106877970>,
<unstructured.documents.html.HTMLListItem at 0x1068776a0>,
<unstructured.documents.html.HTMLListItem at 0x13fe4b0a0>]
```

Run `print("\n\n".join([str(el) for el in elements]))` to get a string representation of the
output, which looks like:

```python
This is a test email to use for unit tests.

Important points:

Roses are red

Violets are blue
```

### Text Document Parsing

The `partition_text` function within `unstructured` can be used to parse simple
text files into elements.

`partition_text` accepts filenames, file-like object, and raw text as input. The following three snippets are for parsing text files:

```python
from unstructured.partition.text import partition_text

elements = partition_text(filename="example-docs/fake-text.txt")

with open("example-docs/fake-text.txt", "r") as f:
  elements = partition_text(file=f)

with open("example-docs/fake-text.txt", "r") as f:
  text = f.read()
elements = partition_text(text=text)
```

The `elements` output will look like the following:

```python
[<unstructured.documents.html.HTMLNarrativeText at 0x13ab14370>,
<unstructured.documents.html.HTMLTitle at 0x106877970>,
<unstructured.documents.html.HTMLListItem at 0x1068776a0>,
<unstructured.documents.html.HTMLListItem at 0x13fe4b0a0>]
```

Run `print("\n\n".join([str(el) for el in elements]))` to get a string representation of the
output, which looks like:

```python
This is a test document to use for unit tests.

Important points:

Hamburgers are delicious

Dogs are the best

I love fuzzy blankets
```


## :guardsman: Security Policy

See our [security policy](https://github.com/Unstructured-IO/unstructured/security/policy) for
information on how to report security vulnerabilities.

## :books: Learn more

| Section | Description |
|-|-|
| [Company Website](https://unstructured.io) | Unstructured.io product and company info |
| [Documentation](https://unstructured-io.github.io/unstructured) | Full API documentation |
