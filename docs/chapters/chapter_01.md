## Bioschemas profiles for training resources

Many training related resources will include pages describing tutorials or courses. As such, they are marked up using the follwoing three profiles:

    `TrainingMaterial`: A profile describing training materials in life sciences, it can be used on its own (as it happens with the Bioschemas tutorials) or in combination with a `CourseInstance`.
    `Course`: A profile describing a course from a generic point of view, i.e., the learning objectives of a course rather than where and when it is delivered.
    `CourseInstance`: A profile describing a particular instance of a course, i.e., an edition of a course that is scheduled for specific dates and happening in a specific location (that of course can be online or on-site, virtual or real).

Note that the `CourseInstance` profile is used in tandem with the `Course` profile, i.e., a `CourseInstance` does not exist without a `Course` but a `Course` can exist without a `CourseInstance` (there are no current offerings of the course).

## Setup of the repository

TODO: add folder structure
TODO: add instruction for publishing mechanism on github

## HTML code for a training material page

Let’s create a new folder called _layouts and have a new empty file called tutorial-event.html inside. This is where our HTML template used to render our tutorial will be.

Open tutorial.html and add the following:

```
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

The annotation with the Bioschemas profile `TrainingMaterial` looks like this:

```
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
This JSON-LD object needs to be inserted in the section `<script type="application/ld+json"> insert JSON-LD object here </script>`. 

TODO: demonstrate tools to edit JSON-LD object template

Once you have inserted the markup (= JSON-LD object), save the file.

## 1.2 HTML code for a training course page
Let’s create a new folder called _layouts and have a new empty file called tutorial-course.html inside. This is where our HTML template used to render our tutorial will be.

Open tutorial.html and add the following:

```
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

You can also embed videos from a local source (with a relative path) or from an url (like youtube). To use a youtube URL, 
just attach the ID of the video to a youtube embedded video link: `https://youtube.com/embed/`. For example, the Elixir training video `https://youtu.be/oAD8FdGf8tI` has the ID `oAD8FdGf8tI`, so the final link would be:

```json
{
   "@context":"https://schema.org/",
   "@type":"Course",
  "http://purl.org/dc/terms/conformsTo":{
    "@type":"CreativeWork",
    "@id":"https://bioschemas.org/profiles/Course/0.9-DRAFT-2020_12_08"
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

![type:video](https://youtube.com/embed/oAD8FdGf8tI)


## 1.3 Publish training course and material via github


## 1.4 Validate the annotation

Validate the individual page with the [schema.org validator](https://validator.schema.org/) by pasting the URL into the Fetch URL tab. The validation procedure will indicate if you have used non-existing properties of the Bioschemas profile. If error messages are returned, have a look at the troubleshooting section below.

TODO: Add image from 

![screenshot of about schema.org validator](./../assets/images/b369eIQ.png)


