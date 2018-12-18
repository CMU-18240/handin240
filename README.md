# 18240 Handin Tool
A handin utility tool for 18240 assignments. Meant to streamline student
workflow with respect to code submissions with the intent of removing Autolab
from the flow entirely, as well as make the lives of the (best) TAs easier. Also
includes some utility scripts that would be useful for the new workflow.

Written in Python, intended for ver. 2.7.5.

## Usage
*TODO*

## Specification
Student workflow should (roughly) be as follows:
1. Do homework involving "PDFed" answers and "Code" answers. Code answers will
be in a set of `.sv`, `.timing`, `.asm`, etc files. There may be multiple code answer
files, of varying types. The PDFed answer file is a scan of the student’s
handwritten work, for instance. **There will only ever be a single PDFed file.**
2. Student places code files in a directory in their own AFS space. This is
probably where they’ve been working anyway, as they need access to VCS, as240,
etc.
3. Student runs our handin script, as they now do. The script is a python
program. We envision lots of cool things that this script will eventually
do.
4. Student discovers there is a new file in the AFS directory - a PDF file
with a name like `HW3_code.pdf`. This file is a "pretty" version of their
code files.
5. Student copies `HWX_code.pdf` to a local machine, where the "PDFed"
file exists.
6. Student goes to gradescope and submits each file to a separate
homework assignment: HW3 and HW3-code, for instance.
7. After homework is graded, they go to gradescope to get their grades on the
two portions of the homework. The HWX-code assignment contains the pretty pdf,
which has been annotated with style or other comments. The HWX-code assignment
has rubrics not only for style, but also for all of the functionality tests that
have been graded.

Some potential features include:
- Detect the student’s Andrew ID
- Check that the current directory is in the student’s space (actually, that
it isn’t in the class space and is a writeable directory)
- Check that each required file exists.
- Copy each required file into the handin directory in the course space
- Use `reportlab` to make a pretty pdf with each code file printed
on a different page.
- Test the file and report results:
    - We will need to find some workaround involving permissions. Students need
      to be able to read the TA testbenches, but if they can then too much
      information would be disclosed. Perhaps a `.svp` inside of the `handout`
      directory is the way to go?
    - What happens here will vary depending on the type of question. At the very
    least, it would check for proper compilation. It could try using our
    testbench on the student’s design. It might use a simple testbench, as
    opposed to a deeper grading testbench.
    - It would be nice if all of the VCS garbage output was captured and parsed
    without the student seeing it.  Ideally, the student would just get a report
    that looks something like:
```
Problem 3: Your file (hw6prob3.sv) does not compile.
Problem 4: 3 of 4 tests passed
Problem 7: File hw6prob7.timing was not found
The file hw6_code.pdf was created. Make sure to submit this file to gradescope!
```

Potential utility scripts that aren't used for students:
- Parse a roster of Andrew IDs to create folders for their submissions for a
  given homework.
- Add the ability to automatically configure `fs` so student has R/W permissions
- Also the ability to disable those permissions once the deadline passes
