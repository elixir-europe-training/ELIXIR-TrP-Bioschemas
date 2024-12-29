## Introduction

[add-bioschemas file='docs/training-material.yaml']

In this scenario, we use a static site generator called Jekyll to transform your plain text into static websites. What are the main component we need to make this basic example work? We need at least one markdown page for the course (overview) which we call index.html, another HTML page tutorial01.html which contains the training material, the rendering mechanism of Jekyll to create and serve the HTML pages on GitHub as web site and ideally a sitemap.xml document to allow easy integration into TeSS.
We have prepared a GitHub repo with files index.html, tutorial01.html, sitemap.xml as well as the other files for Jekyll. The rendering mechanism will be provided by GitHub itself and will be explained later.

## Bioschemas profiles for training resources

Many training related resources will include pages describing tutorials or courses. As such, they are marked up using the following three profiles:

- `TrainingMaterial`: A profile describing training materials in life sciences, it can be used on its own (as it happens with the Bioschemas tutorials) or in combination with a `CourseInstance`.
- `Course`: A profile describing a course from a generic point of view, i.e., the learning objectives of a course rather than where and when it is delivered.
- `CourseInstance`: A profile describing a particular instance of a course, i.e., an edition of a course that is scheduled for specific dates and happening in a specific location (that of course can be online or on-site, virtual or real).

Note that the `CourseInstance` profile is used in tandem with the `Course` profile, i.e., a `CourseInstance` does not exist without a `Course` but a `Course` can exist without a `CourseInstance` (there are no current offerings of the course).

## Setup of the repository

Let's start with the first step and create a new repository from the [basic Bioschemas tutorial template](https://github.com/elixir-europe-training/ELIXIR-TrP-Bioschemas-Jekyll-Template). Once you have opened the link in your browser, you can create a new GitHub repository by clicking on the green 'Use template' button.
Enter a new name for the created repository e.g. ELIXIR-TrP-Bioschemas-Jekyll under your own GitHub account.

## Code for a training material page using Jekyll as static site generator

Let’s create a new folder called _layouts and have a new empty file called tutorial.html inside. This is where our HTML template used to render our tutorial will be.

Open tutorial.html and add the following text:

```html
<!DOCTYPE html>
<html>
  <head>
      <script type="application/ld+json">
         {{ page.bioschemas | jsonify }} 
      </script>
  </head>
  <body>
     {{ content }}
  </body>
</html>
```

This is an example of an HTML file with three HTML elements - `<html>`, `<head>`, and `<body>`. An HTML element is defined by a start tag, some content, and an end tag. For the outer `html` element (`html` is the tagname), the start tag is `<html>` and the end tag is `</html>`. The `/` in front of the tagname indicates an end tag.

The `<html>` element is the root element of an HTML page. The `<head>` element contains meta information about the HTML page and the `<body>` element defines the document's body, and is a container for all the visible contents, such as headings, paragraphs, images, hyperlinks, tables, lists, etc.

TODO: add reference to https://www.w3schools.com/

The markup of the HTML page with the Bioschemas annotation as a JSON-LD object needs to be added to the `<head>` element and be included in a `<script>` element with the attribute `type="application/ld+json"`.

TODO: add markdown file

When using a static site generator like Jeykll, we try to use placeholder (variables) which will be filled in once the static HTML pages are created. In order to facilitate the process, we use a `YAML` header using a `Bioschemas` attribute containing the following properties.

```
bioschemas:
  "@context": https://schema.org/
  "@type": LearningResource
  "http://purl.org/dc/terms/conformsTo":
  - "@type": CreativeWork
    "@id": "https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE"
  about:
    - "@id": https://schema.org
    - "@id": http://edamontology.org/topic_0089
  audience:
  - "@type": Audience
    name: (Markup provider, Markup consumer) WebMaster, people deploying GitHub pages
  name: "Adding Schema.org to a GitHub Pages site"
  author:
  - "@type": Person
    name: "Niall Beard"
    "@id": https://orcid.org/0000-0002-2627-0231
    url: https://bioschemas.org/people/NiallBeard
  contributor:
  - "@type": Person
    name: "Alasdair Gray"
    "@id": https://bioschemas.org/people/AlasdairGray
    url: https://bioschemas.org/people/AlasdairGray
  teaches:
  - "The student will be able to recall shell commands"
  - "The student will be able to write code to copy files"
  - "The student will be able to discover new commands on their own"
  dateModified: 2021-07-22
  description: "This guide will show you how to do add Schema.org markup to a GitHub Pages site."
  keywords: "schemaorg, TeSS, GitHub pages"
  license: CC-BY 4.0
  version: 2.0
```

This `YAML` header is processed by Jekyll to embed the following JSON-LD within the web page. The rather elaborate annotation according to Bioschemas profile `TrainingMaterial` looks like this:

```json
{
  "@context":"https://schema.org/",
  "@type":"LearningResource",
  "@id": "https://example.com/training-material/12345",
  "dct:conformsTo":{
    "@type":"CreativeWork",
    "@id":"https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE"
  },
  "audience":[
    {
      "@type":"Audience",
      "name":"(Markup provider, Markup consumer) WebMaster, people deploying GitHub pages"
    }
  ],
  "description":"This guide will show you how to do add Schema.org markup to a GitHub Pages site.",
  "keywords":"schema.org, TeSS, GitHub pages",
  "name":"Adding Schema.org to a GitHub Pages site",
  "about":[{"@id":"https://schema.org"},{"@id":"http://edamontology.org/topic_0089"}],
  "author":[
    {
      "@type":"Person",
      "name":"Niall Beard",
      "@id":"https://orcid.org/0000-0002-2627-0231",
      "url":"https://bioschemas.org/people/NiallBeard"
    }
  ],
  "educationalLevel":"beginner",
  "identifier": "http://dx.doi.org/12349302",
  "inLanguage": "en-UK",
  "contributor":[
    {
      "@type":"Person",
      "name":"Alasdair Gray",
      "@id":"https://bioschemas.org/people/AlasdairGray",
      "url":"https://bioschemas.org/people/AlasdairGray"
    }
  ],
  "teaches": [
  "The student will be able to recall shell commands", 
  "The student will be able to write code to copy files", 
  "The student will be able to discover new commands on their own"
  ],
  "dateModified":"2021-07-22",
  "license":"CC-BY 4.0",
    "version":2.0
  }
```

This examples uses most of the properties specified in the Bioschemas profile [TrainingMaterial](https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE). 

Once you have inserted the markup (= `YAML` header), save the markdown file file.

Please 

## HTML code for a training course page
Let’s create a new folder called _layouts and have a new empty file called tutorial-course.html inside. This is where our HTML template used to render our tutorial will be.

Open tutorial-course.html and add the following:

```
<!DOCTYPE html>
<html>
  <head>
      <script type="application/ld+json">
         insert Bioschemas annotation here
      </script>
  </head>
  <body>
     insert content here
  </body>
</html>
```

The rather elaborate annotation according to Bioschemas profiles `Course/CourseInstance` looks like this. Note that it is using the annotation for the associated training material, too. This annotation is added via the property `hasPart`.

```json
{
  "@context":"https://schema.org/",
  "@type":"Course",
  "http://purl.org/dc/terms/conformsTo":{
    "@type":"CreativeWork",
    "@id":"https://bioschemas.org/profiles/Course/1.0-RELEASE"
  },
  "description":"ELIXIR Bioschemas Annotation Guide",
  "keywords":"Bioschemas, Schema validation, Harvesting markup, Deploying markup",
  "name":"Bioschemas Annotation Guide for training material",
  "hasPart":[
    {"@type":"LearningResource",
    "@id":"https://dx.doi.org/10.4126/FRL01-006432243",
    "http://purl.org/dc/terms/conformsTo":{
      "@type":"CreativeWork",
      "@id":"https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE"
    },
    "description":"This training material provides a comprehensive guide for annotating websites that host training events and materials. It begins with the basics of website annotation, offering foundational knowledge essential for understanding the process. The course then delves into the specifics of Bioschemas annotation, demonstrating how to apply it to an HTML page to enhance discoverability and interoperability. Following this, the guide explores the integration of Bioschemas with popular static site generators and content management systems, including Jekyll, Mkdocs, and Wordpress. Each section provides practical examples and step-by-step instructions to ensure learners can effectively implement Bioschemas annotations in their own projects. This training is designed to equip participants with the skills needed to improve the visibility and accessibility of their training content on the web.",
    "keywords":"Bioschemas, Schema validation, Harvesting markup, Deploying markup, Training material",
    "name":"ELIXIR Guide for Bioschemas Annotation of Training Assets"
    }
  ],
  "hasCourseInstance":[
    {
      "@type":"CourseInstance",
      "http://purl.org/dc/terms/conformsTo":{
        "@type":"CreativeWork",
        "@id":"https://bioschemas.org/profiles/CourseInstance/1.0-RELEASE"
      },
      "courseMode":"online",
      "location":"Virtual",
      "startDate":"2022-01-10",
      "endDate":"2022-01-10",
      "inLanguage":"en",
      "url":"https://www.workshops.org",
      "instructor":[
        {
          "@type":"Person",
          "name":"Alexander Botzki",
          "@id":"https://orcid.org/0000-0001-6691-4233",
          "url":"https://orcid.org/0000-0001-6691-4233"
        },{
          "@type":"Person",
          "name":"Bruna Piereck",
          "@id":"https://orcid.org/0000-0001-5958-0669",
          "url":"https://orcid.org/0000-0001-5958-0669"
        }
      ]
    }
  ]
}
```

## HTML code for a training material page

Open the tutorial01.html in Edit mode. It has a quite simple structure:

```html
<!DOCTYPE html>
<html>
  <head>
      <script type="application/ld+json">
         insert bioschemas annotation here
      </script>
  </head>
  <body>
     insert content here
  </body>
</html>
```

Since we are annotating a course, we use the Bioschemas profiles `Course/CourseInstance`. The JSON-LD object has several property-value pairs. We have created a table for an easier overview about several important properties we need to fill in or annotate for the Course. If you some explanation about the properties, please have a [detailed look](https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE) on the Bioschemas page.

| property   | values   |
| :--------- | :--------- |
| @contect   | https://schema.org/    |
| @type   | Course    |
| description   | This guide will show you how to do add Schema.org markup to a GitHub Pages site. |
| keywords   | Bioschemas, schema.org, JSON-LD, GitHub pages |
| name   | Adding Schema.org/Bioschemas annotation to a GitHub Pages site |
| educationalLevel  | beginner |
| inLanguage  | en-GB |
| license  |  CC-BY 4.0   |


The rather elaborate annotation according to Bioschemas profile `TrainingMaterial` looks like this:

```json
{
  "@context":"https://schema.org/",
  "@type":"LearningResource",
  "@id": "https://example.com/training-material/12345",
  "dct:conformsTo":{
    "@type":"CreativeWork",
    "@id":"https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE"
  },
  "audience":[
    {
      "@type":"Audience",
      "name":"(Markup provider, Markup consumer) WebMaster, people deploying GitHub pages"
    }
  ],
  "description":"This guide will show you how to do add Schema.org markup to a GitHub Pages site.",
  "keywords":"schema.org, Bioschemas, JSON-LD, GitHub pages",
  "name":"Adding Schema.org to a GitHub Pages site",
  "about":[{"@id":"https://schema.org"},{"@id":"http://edamontology.org/topic_0089"}],
  "author":[
    {
      "@type":"Person",
      "name":"Niall Beard",
      "@id":"https://orcid.org/0000-0002-2627-0231",
      "url":"https://bioschemas.org/people/NiallBeard"
    }
  ],
  "educationalLevel":"beginner",
  "identifier": "http://dx.doi.org/12349302",
  "inLanguage": "en-UK",
  "contributor":[
    {
      "@type":"Person",
      "name":"Alasdair Gray",
      "@id":"https://bioschemas.org/people/AlasdairGray",
      "url":"https://bioschemas.org/people/AlasdairGray"
    }
  ],
  "teaches": [
  "The student will be able to recall shell commands", 
  "The student will be able to write code to copy files", 
  "The student will be able to discover new commands on their own"
  ],
  "dateModified":"2021-07-22",
  "license":"CC-BY 4.0",
  "version":2.0
  }
```
This examples uses most of the properties specified in the Bioschemas profile [TrainingMaterial](https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE). It is quite tedious to create the JSON-LD objects manually, so we would recommend to start from the above example as a template.
  

## Publish training course and material via github

TODO: add content specific for Jekyll

## Validate the markup of the page with the Schema.org validator

Validate the individual page with the [schema.org validator](https://validator.schema.org/) by pasting the URL into the Fetch URL tab. The validation procedure will indicate if you have used non-existing properties of the Bioschemas profile. If error messages are returned, have a look at the troubleshooting section below.

![screenshot of about schema.org validator](https://raw.githubusercontent.com/elixir-europe-training/ELIXIR-TrP-TeSS/refs/heads/main/docs/assets/images/b369eIQ.png)

