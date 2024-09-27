---
layout: default
title: "HCL Domino CompareDBs Template"
nav_order: 1
description: "HCL Domino CompareDBs Template"
has_children: false
---
<h1>HCL Domino CompareDBs Template</h1>

<details close markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

![Screenshot Discussion](assets/images/png/screenshot.png)


## Info

Property | Value
---|---
Filename | comparedbs.ntf 
Templatename | HCL Compare DBs
Template version | 12.0.2
Signed by | Open Source Template/Domino Development
Optimized for | Notes Client 

## What does this application do?

CompareDBs Reports (comparedbs.ntf), installed on the Domino server, can be used to compare two database designs and/or document contents or to analyze the design of one database.
Database comparison You can compare the design of two Notes databases or templates and generate a report that is saved in the database. Some of the options include the ability to:

* Exclude documents from the comparison.
* Integrate the reports that are generated with source control applications such as Git or Jira.
* Use a diff tool of your choice rather than the built-in tabular report that shows differences between source and target.

Database design synopsis You can use the tool to generate a design synopsis of a database that is exported to another database. The target database contains documents describing each design element.

A second template. designsynopsis.ntf, is used to organize and display the design synopsis output as a searchable Notes application.

For complete information on all options and how to get started, use the template to create a new Notes application. (It's an advanced template). Then open the application and select Help > > About This Application and Help > > Using This Application .

## Usage

### Before first use

Each user of this tool needs to set their preferences for how it will work for them on their workstation.
If you have multiple workstations, they will each need this setup done.
In the application navigator, select Configuration > Workstation.

Each user of this tool needs to set their preferences for how it will work for them on their workstation.
If you have multiple workstations, they will each need this setup done.
In the application navigator, select Configuration > Workstation.

**Difference Tool**
When doing comparisons, you can either create a tabular report showing the differences between source and target, or use a file-comparison tool of your choice to view the exported data. This section of the setup lets you select which tools to use and to provide command line options for launching it.
If the design is exported, you get one file per design element, in a folder tree. The working with two databases, the usual operation of this program is to create a report of the differences. However, you may instead (or in addition) use an external tool of your choice to view the differences of the exported application data. The tool you select needs to be able to do a recursive comparison of two folders.
A few popular tools are supported. If you want to use something else, or to modify the default command line arguments for your selected tool, use the Custom option. The command line you define here must include the placeholders %1 and %2, which will be replaced by the source and target export folders.

**Don't Modify Databases in These Folders**
When you access the contents of a Notes database, the file is modified at an operating system level, even if no notes are modified. Opening a database causes the access to be logged, view indexes to be built, tables of notes to be compiled, and so on. All this is technically "touching" the file and changing its contents. If the file was compacted, you've also made it larger again.
If the Notes database is in a folder associated with GIT clone or other source code control system, you generally should avoid modifying these files unintentionally. List the parent folders of such locations in your workstation preferences. Rather than opening them directly, this application will create a temporary file copy of the NSF or NTF and access that copy instead.
This takes longer, of course, and temporarily uses extra disk space. But it lets you do comparisons without worrying about making the SCCS think a Notes application has been modified when it really hasn't.

## Comparing Databases
To compare two databases, in the application navigator select one of the options under COMPARISON. This application is delivered with a couple of styles of comparison, and the application administrator can add more. These choices may differ in the options that are enabled for them. For instance, when comparing two versions of a template you want to compare documents as well as design elements. When comparing a template with a database created from that template, you probably don't want to consider documents.
There are sections of options on this screen that you may want to override in specific situations. These are explained below.
Select the choice that seems best for your situation, then choose the applications you want to compare. This form remembers your previous inputs.
From here, use the Create Report button to compose a document that shows the differences between the applications you selected. This may take some time as all their data must be exported and compared. You can then either save the report in the compareDBs application, or close it without saving. Read more about this report below.
If you prefer to see the differences in a file-comparison tool of your choice, use Launch Diff Tool. You can do both -- the files will only be exported once.
The Export button just generates the design description files in a folder structure, without either launching the diff tool or report.
Once you've exported the files by any of these three methods, you can make a snapshot of the export files using the Save Export... button.

## Report/Submission Form

The form used to present a report of differences, is titled "Submission Report". If this is a report for others to review for a code submission, you can save it (it goes into this database).
If the application administrator has set up for it, you can also select a source code repository and submission number that this report pertains to. For instance if using GIT for source control, this would be the name of the repository and the PR number. When viewing the report, readers will be able to click a link to open the source control record by its URL.
Similarly, if it has been configured by the administrator, you can enter one or more tracking numbers for a task management or bug reporting system. Again, when reading the document, reviewers can click a button to open these tasks or bug reports.

## Generating a Design Synopsis

To create a Notes database containing a description of a database design -- one document per design element -- in the application navigator choose an option under SYNOPSIS. The template comes with a standard Design Synopsis style, and the application administrator may define others for specific situations.
Select the database you want a synopsis of. You may specify multiple paths by entering one per line (in case you have several databases that together comprise a single application). Then click Design Synopsis to generate the output NSF file.
There's a section of options on this screen that you may want to override in specific situations. These are explained below.

## Export Options Explained

The Export options are:
* Export signatures: The output will always include a summary showing how many design elements were signed by what ID. If you check this option, the output for each design element will also include the signer of that design element. Generally you will not want to export signatures when doing comparisons, because often the entire application has been re-signed for a particular environment so every note will be different in this respect. You might really only care whether the design has changed versus the original template. Since the summary information will let you see if there's an unexpected change in how design elements are signed, generally you want to disable this option unless you need to use it to track down which design elements are incorrectly signed.
* Export language: When working with multilingual Notes applications, it's usually helpful to make the output include the language tag of the design element. If the application is not multilingual, or if the language tags have not changed between versions being compared, this will not make your output significantly longer. Generally, enable.
Hide item sign bit: Which items in a design note or document are flagged as eligible for signing, you probably don't care about from the standpoint of function. Generally, enable (i.e. do strip out sign bit from report).
Hide fromtemplate: This DXL attribute reports whether a design element is set to individually inherit its design from a template, and if so which template. Generally you want to disable this option since it does result in potential functional differences and you need to be alerted to the possible nonstandard application of the general design. However, there may be occasions where you really just want to be told about the current difference and ignore design inheritance.
* Export generated .properties: This option applies to multilingual XPages applications. When XPages and Custom Control design elements are saved, their translatable strings are written into design elements that don't show up in the Applications outline of Designer (you can see them in the Navigator view). Generally, this option should be enabled because differences in these files are important to function. However, in some cases, you may not care about these differences. For instance, you've modified the original XPages and haven't done translations yet, so you know very well there will be many properties file changes, but don't need to see those differences in every supported language. Leaving this checked when working with non-Xpages applications doesn't slow things noticeably.
* Compare documents: Profile documents are considered a part of the design and are always exported, but "normal" documents are only included in the export data when this option is checked. You wouldn't normally want this in a design synopsis. You also don't want it when comparing an application with its template, because the application of course will contain a lot of documents that aren't in the template and you don't care about that. But you probably do want to export documents when comparing different versions of a template, because you don't want to accidentally release templates with unintended new documents.
* Export UNIDs: Check this box to include the UNID in the exported information. During a comparison, if the UNIDs are not mostly the same between the two sides, this can result in a very lengthy report showing this one difference for each note which is otherwise identical to its counterpart, so choose wisely. If you're doing a code review of different versions of a template, however, generally you want to know if the UNID of a design element has changed, since this can lead to duplication when replicating with earlier versions of the template.
* Timestamp matching: (for comparison only) Speeds up the comparison process by not bothering to export design elements that have the same "last modified" date. We assume they haven't changed. This is generally a good idea, but if you mean to export the compare results and/or view the DXL of the identical design elements as well as the changed ones, you can disable this option. This option doesn't apply to single-database exports for design synopsis.
* Standardize LotusScript: LotusScript keywords are not case sensitive -- end if and End If work the same. But there is a standard capitalization for LotusScript keywords as you type them. If you copy and paste LotusScript code, it will also be "corrected" to the standard. This change in capitalization doesn't affect functionality, so you generally don't care for code review purposes. This option corrects LotusScript keyword capitalization to the standard, so you don't get hundreds of superfluous differences if you pasted a block of code. The process uses a LotusScript parser to correctly identify which are really keywords as opposed to, e.g. the word "to" appearing within a string literal, so if there's a change to how some text is capitalized, that difference is visible in the report.
* Flag all strings: Used when doing translations, this option puts markers around all static text on form, literal strings in source code, and any other text that might be subject to translation. This is just intended to be used in comparing translated versions of an application. The report phase of the code review operation can detect these string markers and apply highlighting in its report, so reviewers of translation results can easily distinguish between string-related changes and non-string changes.
* Rich text run compaction: In DXL, static text on a form, and certain other elements, are enclosed in <run> elements with enclosed <font> elements and various attributes. This is wordy and can make the actual text hard to distinguish, especially when the rich text "editor" has broken text into multiple runs even though consecutive runs have the same formatting. This tool supports three levels of trimming this down to something more readable.
  * The default, "Compact", removes font elements and includes that information in the run element, removes run elements from around text if the text has the default formatting, and merges consecutive runs if they have the same formatting. Runs that contain no text are removed, even if they have other than the default formatting.
  * The middle level "Show breaks" does the same as compact mode, but inserts a special character to indicate where text was divided into consecutive runs with the same formatting. This is helpful information if using a translation tool, such as Domino Global Workbench, that cares about this, or if you want to be wary of breaks that may occur in the middle of a word, leading to text wrapping inappropriately ar that point.
  * The "Verbose" option doesn't touch anything, giving you the original DXL. This is hard to read and seldom helpful, but if you want to make extra sure there's not (let's say) an addition of an empty text run with a large font size that might affect the line height at that point, this is a way to find that type of difference. Mostly you would only do this if you made such a change on purpose and wanted to make sure the difference report showed what you did. NOTE: adding empty runs is not the recommended way to adjust line heights.
* Form key fields: used when exporting documents to calculate a hopefully unique "key" for each document. For instance, you might want to say, "If Form = 'CatalogItem', use field ItemID as the key, if Form = 'Order', use OrderNum, ...". The comparison report will match documents by their keys, so this is important for doing comparisons in cases where the UNIDs of documents don't necessarily match. The value calculated here is used as the filename for exported DXL files, and the subject line in documents exported to a design synopsis. The Compare Configuration form contains help and examples of how to specify this information. Of course, this can depend what application you're scanning, so entering special values here may often be associated when creating custom compare configurations for specific tasks.
* Fallback key formula: Specifies how to generate keys for documents that don't match any of the form key values. Generally this would use the document Universal ID to provide a match unless a Subject or Name field is available.

#### Report Options
The report options only apply to two-database comparisons (not to design synopsis). These options are:
* Ignore case differences: generally, case does matter, but you have the option to disregard that if it produces too long a report. Most often, the case differences you don't care about are in LotusScript reserved words, and there's a separate option for that in the Export options. Usually, don't ignore case differences.
* Ignore indentation differences: The DXL output is "pretty printed" in a standard way, so whitespace differences at the beginning of a line are generally irrelevant and this option should be enabled by default. If a field is moved into a table cell, for instance, its indentation will be different but if the field design hasn't changed, we don't want every line flagged as different -- just to show the addition of the containing table elements above and below the field.
* Line numbers: The line numbers refer to the position of the lines within the exported DXL data. This is generally enabled. These numbers are useful during code reviews to reference the location of the difference in the report.
* New files: Tells what to do about any design elements or documents that appear on the "right" side of the comparison (assumed to be the newer version) but not the "left" (the presumed older version). These notes have been "added". The "List filenames" choice just adds their titles to the report. The "Attach files" choice adds the titles to the report and also attaches the DXL files and other files as file attachments in the report. The "Embed contents" choice lists the new items in the report, and also puts the actual text of the DXL description into the report instead of an attachment. Image resources and other non-text files are still done as attachments.  Generally, "Embed" is the best choice for code reviews, because reviewers can see everything by just scrolling and use Ctrl+F to find words in the report. However, if there's a lot of new design, this can result in a report that's too long to be displayed as Notes rich text. If you have a problem, use one of the other options.
* Abbreviate left...: If you deleted something from the left-side database in a comparison, it's generally not necessary to display the entirety of the deleted information on the left side of the report. This field lets you set the maximum length of deleted data to display in full per single block in the left column. If it's longer than that, text will be taken out of the middle and replaced with a "text omitted here" marker. If you want to always display the deleted data in full, put a large number here.
* Context lines: controls how many lines of identical DXL data to display before and after the point where a difference was found. 3 lines is typically enough for people to tell what's going on, but you may need to change it for individual cases.

## Application Setup / For Admins

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