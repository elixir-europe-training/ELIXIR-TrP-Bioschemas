## Bioschemas profiles for training resources

[add-bioschemas file='docs/training-material.yaml']

Many training related resources will include pages describing tutorials or courses. As such, they are marked up using the following three profiles:

- `TrainingMaterial`: A profile describing training materials in life sciences, it can be used on its own (as it happens with the Bioschemas tutorials) or in combination with a `CourseInstance`.
- `Course`: A profile describing a course from a generic point of view, i.e., the learning objectives of a course rather than where and when it is delivered.
- `CourseInstance`: A profile describing a particular instance of a course, i.e., an edition of a course that is scheduled for specific dates and happening in a specific location (that of course can be online or on-site, virtual or real).

Note that the `CourseInstance` profile is used in tandem with the `Course` profile, i.e., a `CourseInstance` does not exist without a `Course` but a `Course` can exist without a `CourseInstance` (there are no current offerings of the course).

## Introduction

What are the main component we need to make this basic example work? We need at least one HTML page which we call index.html, a rendering mechanism to serve the HTML page as web site and ideally a sitemap.xml document to allow easy integration into TeSS.
We have prepared a github repo with these two files index.html and sitemap.xml. The rendering mechanism will be provided by github itself and will be explained later.

## Setup of the repository

Let's start with the first step and create a new repository from the [tutorial template](https://github.com/elixir-europe-training/ELIXIR-TrP-Bioschemas-HTML-Template). Once you have opened the link in your browser, you can create a new github repository by clicking on the green 'Use template' button.
Enter a new for the created repository e.g. ELIXIR-TrP-Bioschemas-HTML under your own github account.

We anticipate the following basic setup: we have one HTML page which describes the course aka the training event called index.html and one HTML file tutorial01.html for the training material. 

## HTML code for a training course page

Open the index.html with Edit mode on Github. It has a quite simple structure: 

```
<!DOCTYPE html>
<html>
  <head>
      <script type="application/ld+json">
         insert Bioschemas annotation about course here
      </script>
  </head>
  <body>
     <h2 id="lesson-overview">Lesson overview</h2>
     ...
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
  "description":"Bioschemas Tutorial at SWAT4HCLS Leiden",
  "keywords":"Bioschemas, SWAT4HCLS, Schema validation, Harvesting markup, Deploying markup",
  "name":"Bioschemas - Deploying and Harvesting Markup",
  "hasPart":[
    {"@type":"LearningResource",
    "@id":"https://dx.doi.org/10.4126/FRL01-006432243",
    "http://purl.org/dc/terms/conformsTo":{
      "@type":"CreativeWork",
      "@id":"https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE"
    },
    "description":"Bioschemas Tutorial at SWAT4HCLS Leiden",
    "keywords":"Bioschemas, SWAT4HCLS, Schema validation, Harvesting markup, Deploying markup",
    "name":"Bioschemas - Deploying and Harvesting Markup"
    }
  ],
  "hasCourseInstance":[
    {
      "@type":"CourseInstance",
      "http://purl.org/dc/terms/conformsTo":{
        "@type":"CreativeWork",
        "@id":"https://bioschemas.org/profiles/CourseInstance/0.8-DRAFT-2020_10_06"
      },
      "courseMode":"online",
      "location":"Virtual, and Fletcher Wellness-Hotel, Leiden, The Netherlands",
      "startDate":"2022-01-10",
      "endDate":"2022-01-10",
      "inLanguage":"en",
      "url":"https://www.swat4ls.org/workshops/leiden2022/",
      "instructor":[
        {
          "@type":"Person",
          "name":"Alban Gaignard",
          "@id":"https://bioschemas.org/people/AlbanGaignard",
          "url":"https://bioschemas.org/people/AlbanGaignard"
        },{
          "@type":"Person",
          "name":"Leyla Jael Castro",
          "@id":"https://bioschemas.org/people/LeylaGarcia",
          "url":"https://bioschemas.org/people/LeylaGarcia"
        },{
          "@type":"Person",
          "name":"Alasdair Gray",
          "@id":"https://bioschemas.org/people/AlasdairGray",
          "url":"https://bioschemas.org/people/AlasdairGray"
        }
      ]
    }
  ]
}
```

TODO: add explanation of the various properties and reference the extensive documentation of the Bioschemas profile.

## HTML code for a training material page

Open the index.html in Edit mode. It has a quite simple structure:

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

All HTML documents must start with a <!DOCTYPE> declaration. The declaration is not an HTML tag. It is an "information" to the browser about what document type to expect.

This is an example of an HTML file with three HTML elements - `<html>`, `<head>`, and `<body>`. An HTML element is defined by a start tag, some content, and an end tag. For the outer `html` element (`html` is the tagname), the start tag is `<html>` and the end tag is `</html>`. The `/` in front of the tagname indicates an end tag. 

The `<html>` element is the root element of an HTML page. The `<head>` element contains meta information about the HTML page and the `<body>` element defines the document's body, and is a container for all the visible contents, such as headings, paragraphs, images, hyperlinks, tables, lists, etc.

Now, let's focus on the markup of the HTML page. There are several technical options to markup an HTML file, we focus on using a [JSON-LD](https://en.wikipedia.org/wiki/JSON-LD) object in combination with a [Bioschemas](https://bioschemas.org/) annotation.

As you see in the code example above, the markup of the HTML page with the Bioschemas annotation as a JSON-LD object needs to be added to the `<head>` element and be included in a `<script>` element with the [attribute](https://www.w3schools.com/html/html_attributes.asp) `type="application/ld+json"`.

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
This examples uses most of the properties specified in the Bioschemas profile [TrainingMaterial](https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE). It is quite tedious to create the JSON-LD objects manually, so we would recommend to start from the above example as a template.

TODO: demonstrate tools to edit JSON-LD object template

In the example code, replace `insert bioschemas annotation here` by the JSON-LD object and save the HTML file.

## 1.3 Publish training course and material via github

TODO: add content from https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site

## 1.4 Validate the annotation

Validate the individual page with the [schema.org validator](https://validator.schema.org/) by pasting the URL into the Fetch URL tab. The validation procedure will indicate if you have used non-existing properties of the Bioschemas profile. If error messages are returned, have a look at the troubleshooting section below.

TODO: Add image from TeSS course

![screenshot of about schema.org validator](./../assets/images/b369eIQ.png)

TODO: add reference to https://www.w3schools.com/

