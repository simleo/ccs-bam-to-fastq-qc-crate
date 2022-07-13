# ccs-bam-to-fastq-qc-crate

[Workflow Testing RO-Crate](https://crs4.github.io/life_monitor/workflow_testing_ro_crate) setup for [CCS.BAM to FASTQ + QC](https://workflowhub.eu/workflows/220).

## Steps followed

* Installed Python prerequisites with `pip install planemo repo2rocrate`.
* Clicked on the "Run on usegalaxy.eu" on the [workflow's page](https://workflowhub.eu/workflows/220) in WorkflowHub to import the workflow in Galaxy Europe.
* Uploaded [ce#unmap2.bam](https://github.com/samtools/samtools/blob/1224ffbfa249f4e602840e1723bd824c148e0b7d/test/mpileup/ce%23unmap2.bam) to Galaxy to be used as an input file.
* Ran the workflow on Galaxy and retrieved the invocation id from the Workflow Invocations page (User > Workflow Invocations).
* Ran `planemo workflow_test_init --galaxy_url https://usegalaxy.eu --from_invocation <INVOCATION_ID> --galaxy_user_key <GALAXY_API_KEY>` (User > Preferences > Manage API Key). This generates an first version of the test setup including: the workflow file; a test-data directory containing the input and all outputs; the Planemo configuration file. The latter specifies an exact comparison of all output files with the expected ones (i.e., the ones under test-data, taken from the specified invocation).
* Edited the test setup, changing some file names (note that if the workflow is named `xyz.ga`, the Planemo configuration file must be called `xyz-tests.yml`) and the configured checks (some outputs are in a free text format that may easily change between releases or even invocations, so an exact comparison would not be appropriate).
* Added a simple GitHub Action workflow to run the test under `.github/workflows/wftest.yml`.
* Generated the crate with `repo2rocrate`:

```
repo2rocrate \
  --repo-url https://github.com/simleo/ccs-bam-to-fastq-qc-crate \
  -o ccs-bam-to-fastq-qc.crate.zip
```

* Uploaded the zipped crate to LifeMonitor ([dev instance](https://app.dev.lifemonitor.eu/)).

## Copyright info

The Galaxy workflow `bam-to-fastq-qc.ga` has been copied from [CCS.BAM to FASTQ + QC at version 1](https://workflowhub.eu/workflows/220?version=1), created by Gareth Price and licensed under the [GNU General Public License v3.0 or later](https://spdx.org/licenses/GPL-3.0-or-later.html).

The input data file `test-data/ce#unmap2.bam` has been copied from [samtools@1224ffb](https://github.com/samtools/samtools/blob/1224ffbfa249f4e602840e1723bd824c148e0b7d/test/mpileup/ce%23unmap2.bam), distributed under the following [license](https://github.com/samtools/samtools/blob/1224ffbfa249f4e602840e1723bd824c148e0b7d/LICENSE):

```
The MIT/Expat License

Copyright (C) 2008-2022 Genome Research Ltd.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL
THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.


[The use of a range of years within a copyright notice in this distribution
should be interpreted as being equivalent to a list of years including the
first and last year specified and all consecutive years between them.

For example, a copyright notice that reads "Copyright (C) 2005, 2007-2009,
2011-2012" should be interpreted as being identical to a notice that reads
"Copyright (C) 2005, 2007, 2008, 2009, 2011, 2012" and a copyright notice
that reads "Copyright (C) 2005-2012" should be interpreted as being identical
to a notice that reads "Copyright (C) 2005, 2006, 2007, 2008, 2009, 2010,
2011, 2012".]
```
