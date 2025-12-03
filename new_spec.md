(new-spec)=
# Contributing new specifications

ORMIR-MIDS is meant to be a standard that adapts with the necessities of the community. The specifications for nonstandard or more complex acquisition types are collected in separate files in the `specs` directory of the [website repository](https://github.com/ormir-mids/ormir-mids.github.io).

## Why contribute?

As ORMIR, we decided not to be prescriptive and try to cover all possible use cases of ORMIR-MIDS, but rather focus on the modalities and acquisition types that we, as members, use. If your particular MR sequence or imaging modality is not covered, it's the perfect occasion for you to propose new guidelines!

## Writing your own specification file

If you would like to propose a specification for a new modality, clone the repository and add a markdown file in the specs directory. The name of the file should be something descriptive, and the format should be similar to the following:

```
# (MODALITY) Acquisition type

```{list-table}
:header-rows: 1

* - Imaging method
  - Folder name
  - File name suffix
  - Image volume
  - JSON fields
* - <ACQUISITION TYPE>
  - <folder>
  - <suffix>
  - <dimensionality>
  - <JSON fields required>
```

This creates a file with a title, and a standardized table that provides the required information.

Add any advanced instructions after the table.

## Creating a pull request

After you have created this specification file into your own clone of the repository, you can [create a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) to start the discussion about the new guidelines within the community.
