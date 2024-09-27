---
layout: default
title: "Setup"
parent: "HCL Domino CompareDBs Template"
nav_order: 1
description: "Setup"
has_children: false
---
<h1>Setting up the HCL Domino CompareDBs Tool</h1>

<details close markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>


## Application Setup

Before first use of this application, an application administrator needs to provide information about systems used internally for source control and task tracking.
In the navigation outline, go to CONFIGURATION > Application.
Each code review report can potentially be related to multiple tasks in multiple task tracking systems. Task ID URLs lets you define a mapping between task/defect IDs and the URLs of those tasks or defects. To do this, write a formula to translate a task or defect ID into the URL where that task record can be viewed. The form gives guidance and some example formulas for situations of single vs. multiple task tracking systems. When writing Notes URLs, make use of the fact that the document ID portion of a Notes URL can use a key value from the first sorted column of the view (as an alternative to the document Universal ID).
This tool is designed under the assumption that each code review report is associated with a single submission in your SCCS (source code control system), but you may have reports for multiple SCCS within the same reports database. So when creating a report, the user can specify which repository the report relates to, and the ID of the submission within that repository (for instance, if using GIT, this would be the PR number).
The Source Code Control System Names field lets you define a list of SCCS repositories that this application is associated with, and for each one lets you supply a URL syntax for navigating to that record in the repository. So this is a list of keyword values for SCCS names, and the associated URLs for those systems. You can use whatever names are meaningful to your users -- they will select from among a keyword list of those values when editing the report document.

### Creating Additional Compare and Design Synopsis Types

Because comparisons can be run for different purposes, the tool supports several options for how it manipulates raw DXL output to produce the final exported data. You might, for instance, want different options if doing a comparison for code review on template changes, versus comparing a standard template design with your customized version of that same template, versus seeing how the data in certain documents has changed. These options are described above.
The template ships with a few generic "compare types" giving typical option sets for a normal code review of consecutive versions of an application, original template versus modified application, and for a standard design synopsis.
Navigate to **CONFIGURATION > Compare Types** to view and customize these options, or to define your own specialized comparison or synopsis option sets. If you create new "compare configurations", they appear as options for the end user in the application's main navigation.
Users can override any option; these settings just provide your standard defaults so they can run a report without have to think each time about each option.
There are two basic types of configurations -- the Design synopsis, where the user will just export a description of the design and documents into an NSF they specify, and Compare, where they provide pairs of databases to view just their differences as opposed to the whole design. The Compare Configuration form has this selection.