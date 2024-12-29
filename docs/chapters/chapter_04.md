## Introduction

If you use WordPress as the content management system, there a many possibilities how the content of the course announcement as well as the content of the tutorial aka the training material is provided. This is why we only describe a plugin with which you can markup your WordPress pages. It is a commercial plugin from RankMath.

## Bioschemas profiles for training resources

[add-bioschemas file='docs/training-material.yaml']

Many training related resources will include pages describing tutorials or courses. As such, they are marked up using the following three profiles:

- `TrainingMaterial`: A profile describing training materials in life sciences, it can be used on its own (as it happens with the Bioschemas tutorials) or in combination with a `CourseInstance`.
- `Course`: A profile describing a course from a generic point of view, i.e., the learning objectives of a course rather than where and when it is delivered.
- `CourseInstance`: A profile describing a particular instance of a course, i.e., an edition of a course that is scheduled for specific dates and happening in a specific location (that of course can be online or on-site, virtual or real).

Note that the `CourseInstance` profile is used in tandem with the `Course` profile, i.e., a `CourseInstance` does not exist without a `Course` but a `Course` can exist without a `CourseInstance` (there are no current offerings of the course).

## Setup of the WordPress CMS

We do not describe the way to setup a WordPress sandbox system since it is beyond the scope of this tutorial.

### Configuration of the Bioschemas Profile as Schema template

1. Install the [RankMath SEO and RankMth SEO Pro plugins](https://rankmath.com/).
2. After successfull installation, in the RankMath menu, go to `Schema templates`.
3. Click on `Add New Schema`
4. Click on `Import` in the Schema Generator dialogue
5. Select the `JSON-LD/Custom Code` option in the dropdown of the `Import Schema Code from` field.
6. Copy and paste the template below in the empty `Custom JSON-LD Code` field.
7. Click on the `Process Code`
8. Click on `Use`
9. Check the `Display Conditions` field to potentially exclude certain `Post types` of the Wordpress system

Template for Bioschemas TrainingMaterial profile:

```json
{
  "@context": "https://schema.org",
  "@graph": {
    "@type": "LearningResource",
    "@id": "%url%",
    "dct:conformsTo": {
      "@type": "CreativeWork",
      "@id": "https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE"
    },
    "name": "%seo_title%",
    "url": "%url%",
    "description": "%seo_description%",
    "keywords": [
      "AlphaFold Database (13181)",
      "second keyword",
      "third keyword"
    ],
    "author": [
      {
        "@type": "Person",
        "name": "%post_author%"
      },
      {
        "@type": "Person",
        "name": "Alexander Botzki | https://orcid.org/0000-0001-6691-4233"
      }
    ],
    "contributor": [
      {
        "@type": "Person",
        "name": "Kenneth Hoste"
      }
    ],
    "audience": [
      {
        "@type": "Audience",
        "audienceType": "Life scientists with programming skills"
      }
    ],
    "about": [
      {
        "@type": "DefinedTerm",
        "@id": "http://edamontology.org/topic_2814",
        "inDefinedTermSet": "http://edamontology.org",
        "name": "Protein structure analysis",
        "url": "http://edamontology.org/topic_2814"
      },
      {
        "@type": "DefinedTerm",
        "@id": "http://edamontology.org/topic_3474",
        "inDefinedTermSet": "http://edamontology.org",
        "name": "Machine learning",
        "url": "http://edamontology.org/topic_3474"
      },
      {
        "@type": "DefinedTerm",
        "@id": "http://edamontology.org/topic_0082",
        "inDefinedTermSet": "http://edamontology.org",
        "name": "Structure prediction",
        "url": "http://edamontology.org/topic_0082"
      }
    ],
    "license": "https://spdx.org/licenses/CC-BY-NC-SA-4.0.html",
    "educationalLevel": "intermediate",
    "dateCreated": "%date%",
    "learningResourceType": "hands-on tutorial",
    "inLanguage": "en-GB",
    "version": "1.0"
  }
}
```

Template for Bioschemas Course/CourseInstance profile:

```json
{
  "@context": "https://schema.org",
  "@graph": {
    "@type": "Course",
    "@id": "%url%",
    "dct:conformsTo": {
      "@type": "CreativeWork",
      "@id": "https://bioschemas.org/profiles/Course/1.0-RELEASE"
    },
  "description": "%seo_description%",
  "keywords":"Bioschemas, SWAT4HCLS, Schema validation, Harvesting markup, Deploying markup",
  "name": "%seo_title%",
  "hasCourseInstance":[
    {
      "@type":"CourseInstance",
      "@id": "%url%",
      "http://purl.org/dc/terms/conformsTo":{
        "@type":"CreativeWork",
        "@id":"https://bioschemas.org/profiles/CourseInstance/1.0-RELEASE"
      },
      "courseMode":"online",
      "location":"Virtual, and Fletcher Wellness-Hotel, Leiden, The Netherlands",
      "startDate":"2022-01-10",
      "endDate":"2022-01-10",
      "inLanguage":"en-GB",
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
          "name":"%post_author%",
          "@id":"https://bioschemas.org/people/AlasdairGray",
          "url":"https://bioschemas.org/people/AlasdairGray"
        }
      ]
    }
  ]
}
```
For further reference, RankMath has provided [step-wise procedures](https://rankmath.com/kb/schema-generator/) for configuring the schema.org templates.

### Configure the Sitemap for your WordPress system

0. Check whether the sitemap option needs to be activated in the General configuration of the RankMath plugins.
1. In the RankMath menu, go to `Sitemap Settings`.
2. In the `General` section, the URL to the sitemap is displayed: `Your sitemap index can be found here: https://your.url.org/sitemap_index.xml`
3. Manually check all the sections on the left side of the displayed website from `HTML Sitemap` over all `Post Types` and `Taxonomies`. Unselect the slider for all non-relevant Post types and Taxonomies.
4. Verify the URL whether all relevant links to the pages are shown.

## Finetuning of markup for a training material page

1. When using the Gutenberg editor, you will see a RankMath button in the top right corner of the post you would like to edit.
2. Click on the Schema icon (third from the left) which looks like a certificate.
3. Click on the blue button `Schema Generator`
4. Click on `Your templates`
5. Click on `LearningResource` which is shown in the list of our own templates.
6. In the subsequent dialogue, overwrite the relevant properties from the template with values specific to your training material.
7. Check the reference RankMath has provided [step-wise procedures](https://rankmath.com/kb/schema-generator/) on how to add properties if needed.
8. Click on the blue button `Save for this post` at the bottom of the dialogue. 

RankMath has provided articles in their knowledgebase about finetuning the markup of WordPress posts [here](https://rankmath.com/kb/rich-snippets/).

## Validate the markup of the page with the Schema.org validator

Validate the individual page with the [schema.org validator](https://validator.schema.org/) by pasting the URL into the Fetch URL tab. The validation procedure will indicate if you have used non-existing properties of the Bioschemas profile. If error messages are returned, have a look at the troubleshooting section below.

In this scenario, you can validate the course web site (TODO: add link) and individual tutorial web site (TODO: add link). 

![screenshot of about schema.org validator](https://raw.githubusercontent.com/elixir-europe-training/ELIXIR-TrP-TeSS/refs/heads/main/docs/assets/images/b369eIQ.png)

